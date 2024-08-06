 - Hugging face içinde türkçe sentence transformerları şu şekilde listeleniyor:
	 - ![[Pasted image 20240730162858.png]]
	 - Bu modeller arasında en iyi modeller işaretliler. En üstteki ve en çok indirilen için hangi model olduğu explicitliy specify edilmemiş ama yılını düşününce BERTurk olma ihtimali daha yüksek
	 - Alttaki ise ytu-ce-cosmos/turkish-medium-bert-uncased üzerine fine tune edilmiş
	 - Tüm modellerde kullanılan datasetleri aynı: 
		 - ![[Pasted image 20240730163153.png]]
	 - Bunlar arasında en çok indirilen "emrecan/bert-base-turkish-cased-mean-nli-stsb-tr"
	 - Buna dair detaylar için [[Emrecan Türkçe Sentence Transformers| şuraya]] yönelebilirsin.
	 - niye var olan ingilizce için train edilmiş bir sentence transformer'ı pretrain edip fine tune etmiyoruz
multilingual model:  https://huggingface.co/sentence-transformers/paraphrase-multilingual-MiniLM-L12-v2


## Possible Pathways
- [ ] Türkçe sentence transformers modeli inference alma
- [ ] Türkçe sentence transformers modeli kötü çalışıyorsa domain adaptation yapılabilir
- [ ] XLM-Roberta gibi multilingual transformer modelleri sentence transformer olarak train edilebilir
- [ ] Multilingual sentence transformer modellerinde inference denenebilir. Düşük skor alınırsa domain adaptation, fine-tuning vs. yapılabilir
- [ ] Türkçe transformers modeli sentence transformers olarak eğitilebilri


## Türkçe sentence transformers modeli inference deneyleri
 - [[oquzhansahin | oguuzhansahin/bi-encoder-mnrl-dbmdz-bert-base-turkish-cased-margin_3.0-msmarco-tr-10k ]]
 - [[emrecan | emrecan/bert-base-turkish-cased-mean-nli-stsb-tr]]
 - atasoglu/turkish-base-bert-uncased-mean-nli-stsb-tr
