- model name: Alibaba-NLP/gte-multilingual-reranker-base
	- 305M parametre
	- result return time (Colab): approximately 0.05 sec
	-  Cross-encoderla 4970 query için retrieve edilen her 10 contexti  rerank yaptırdım. Ortalama 0.011 saniye içinde bir query i 10 context ile karşılaştırabiliyor.
	- Map@10 scoreu 0.73'ten 0.79 a çıkıyor.
	- ![[Pasted image 20240906113622.png]]
- model name: amberoad/bert-multilingual-passage-reranking-msmarco
	- 167M parametre
	- result return time (Colab): approximately 0.04 sec
- model name: ytu-ce-cosmos/turkish-small-bert-uncased
	- 29M parametre
	- result return time (Colab): approximately 0.015 sec


-


- [ ] hangi chunkalrı döndüpünü bastır
- [x] ~~bu pipeline ı nasıl improve edebilirsin fikir üret~~
- [ ] biencoder cpu da dene benchmark bak
- [ ] pazartesi ne yapmak istediğime ve hangisiini hangi öncelikle belirlediğime dair yönerge paylaş.
- [ ] lamgchain üzerinden giderek implementasyonunu anlat

