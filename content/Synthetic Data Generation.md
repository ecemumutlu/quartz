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