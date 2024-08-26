Kaynaklar
- [Synthetic DATA Generation using LANGCHAIN 🦜️🔗](# Synthetic DATA Generation using LANGCHAIN 🦜️🔗)
	- Related ipynb [notebook](https://github.com/sudarshan-koirala/youtube-stuffs/blob/main/langchain/synthetic_data_generation.ipynb)
- [How to use LLAMA3.1 with LANGCHAIN for free](https://www.youtube.com/watch?v=jP2llR7ZtwM)
- Langchain Synthetic data generation example [scripts](https://python.langchain.com/v0.1/docs/use_cases/data_generation/)
- Kullanılan dataset: https://huggingface.co/datasets/musabg/wikipedia-tr


Yorumlar
- Datasetinin her bir entrysindeki textleri daha küçük chunklara ayırdım. Chunkların her biri en az 320 kelimeden oluşacak şekilde paragraflarla split edildi.
- Her bir entry için random olarak bir tane chunk'ı context olarak seçip yeni oluşturduğum "context" column'unda kaydettim.
- **Langchain** kullanarak **llama-3.1-70b-versatile** modelini **groq** yardımıyla bu entrylerin ilk 4970 tanesi için question ürettirdim. 
- Elimdeki verileri Multilingual bir sentence transformers modeli olan AlibabaNLP ile test ettim.
- 4970 entry ve tüm entrylerin ilk 50k sı vector database olarak kullanılarak alınan sonuç şu şekilde:
	- Relevant answer in first answer:  3358 / 4970
	- Relevant answers in top-5:  3995 / 4970
- Yukarıdaki veriler doğrultusunda model yetersiz bulunursa daha çok sentetik question ürettirilerek finetune alınabilir.


todo:
- [x] Inference sonuçları metriklerine bak (wikirag-tr, outpus.json, sentetik veri)
	- [x] map@1 
	- [x] map@5 
	- [ ] ndcg@5 -> ndcg@k hesaplamak için yeterince **gerçek** değer yok. Şuanki datasetlerinde her birinin **sadece 1 tane gerçek context eşleşmesi** var. Yani @k içinde bir relevancy sırası yapamıyoruz
	- [ ] ndcg@10 
- [ ] finetune alıp performans iyileşmesi oluup olmadığına bak
- [ ] iyileşme durumuna hem wikirag-tr hem output.json a bak


## Alibaba-NLP/gte-multilingual-base inference sonuçları

| **datasets / metrics** | **map@1** | **map@5** | **ndcg@5** | **ndcg@10** |
| :--------------------: | :-------: | :-------: | :--------: | :---------: |
|    **output.json**     |   0.41    |   0.59    |     x      |      x      |
|     **wikirag-tr**     |   0.66    |   0.82    |     x      |      x      |
|   **sentetik_4970**    |   0.68    |   0.73    |     x      |      x      |
