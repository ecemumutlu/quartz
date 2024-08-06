
 - Datasetleri
	 1. Wiki-rag dataseti: https://huggingface.co/datasets/Metin/WikiRAG-TR
	 2. Wiki-tr dataseti (RAG ile alakası yok): https://huggingface.co/datasets/musabg/wikipedia-tr
 - Datasetlerinin şöyle problemleri var:
	 - 1. datasetinde yalnızca 6000 row var. Her bir row içinde farklı contextlerin birleştiği bir context havuzu var. Bunları ayrı contexlerine ayırıp baktığımda yaklaşık 12500 farklı context çıkıyor. Ama contextler hep kısa kısa. Tüm wiki sayfası paylaşılmamış da direkt query ile alakalı olan kısım konulmuş sadece.
	 - Yukardaki durum göz önünde bulundurulunca aranan query ile eşleşen zaten çok az context olduğu için direkt istenen contexti dönüyor. Yani inference aldığımız modelin iyi çalışıp çalışmadığına dair biz gözlem yapamıyoruz.
	 - Ama zaten gerçek hayatta kullanacağımız bir RAG applicationda da farklı konuların olduğu daha sparse bir vector database'imiz olması daha olası. O yüzden bu bir problem yaratmayabilir.
	 
	 - 2. dataseti RAG için ayarlanmış değil. O yüzden sentetik RAG datası üretmek adına wiki entry leri kullanılabilir. Şu şekilde chatgpt'ye bir prompt verdim: https://chatgpt.com/share/d42fed87-bc30-4a32-9e7e-c9dd88146adc
	 - Bu promptu kullanarak sentetik query ürettirebilriz. Few-shot için verdiğim verileri 1.datasetinden kullandım.

 - Çözüm fikirleri:
	 1. 2. dataseti için sentetik veri üretmek
	 2. 1. datasetindeki contextlerin her birinin alındığı wiki girdilerini bulup llm'e tüm contexti vermek
	 3. 1.dataset contextleri ile 2.dataset contextlerini birleştirip 1.dataseti questionlarını aratmak


 - Genel sorular:
	 1. Eğer domain specific sorularla karşı karşıyaysak kullandığımız sentence transformers embedding modeli fine-tune edilebilir.
	 2. Advanced retrieval teknikği uygulanacaksa belki context summarization yapılıp vector database'e o embed edilebilir.
	