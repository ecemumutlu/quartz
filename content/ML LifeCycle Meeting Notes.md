## Business Requirements
Örnek case: Kedi köpek sınıflandırması
	Kedi ve köpeklerin barınaklarda girdikleri klübeler var.
	Köpek klübesi köpek görünce kapısı açılıyor. Kedi görünce açılmıyor.
	Kedi klübesi kedi görünce kapısı açılıyor. Köpek görünce açılmıyor.

business gereksinimleri ile bilimsel yaklaşımı birleştiren veri bilimcisi oluyor.

ML system users: kullanıcılar, stakeholders
	burada sadece sistemin yapılmasını isteyenler değil sistemi kullanabilecek herkesin düşünülmesi lazım -> mesela barınaktan hayvan sahiplenecek kişiler vs

Peki nasıl bir başarı oranı aranıyor: %90 true positive isteniyor olabilir
	Sistemde nasıl bir başarı almamız gerektiğinin belirtilmesi lazım
		MEsela 1 sn de 20 frame forward pass edebiliyor olsun ve hepsinden %90 üstü accuracy alabilsin - 20fps %90 accuracy başarısı istenşyor olsun
		


İlk problem tanımı yapılmalı:
	Makine öğrenimine gereksinim yoksa kullanmayalım!
	İnsan bazlı kodlanabilir değilse zor bir problemdir -> Makine öğrenmesi gerekebilir

Mesela bizim case'imizde problem bir sınıflandırma. Detection değil (localization bazlı değil)
	1. Cat vs Dog classification
	2. Cat vs Dog vs Other classification
	3. Cat vs Other classification + Dog vs Other Classification

Artık neyle çözebileceğimize dair bir fikrimiz var


## Infrastructure
Sistem hangi device üzerinde çalışacak
Case: Mesela klübenin üzerinde çalışsın ama pahalı bir device olmasın diyor -> edge device kullanımı **Edge Development** 
	Onnx cihaz + tensorRT engine -> python seviye kodu c ye çekiyor
	Quantization -> gereksiz 0 lardan kurtulmak (compact) 
	Pruning -> gereksiz leaflerden kurtulmak


## Data
Klübenin önünden bir kamerayla kedi köpek göreceksen internetten topladığın ışık vs gibi etkenler accuracy f1 düşürebilir. Bulduğun data bu yüzden önemli. Gerçek case'te nelerle karşılaşacağını düşünüp data bulman lazım.

**Mümkünse alandan veri topla**
	Veri toplamak için setup kurup data toplanır.


## ML Algorithms
### Transfer learning
Domain çok uzak değilse freeze edilecek layer sayısı çok az olmalı

## Evaluation
Data evaluation
Performance Evaluation
Liability Evaluation 
	-> model performansının uçlarını test ediyor
	-> çamur geldi kameraya, yağmur yağdı vs bu caselerde nasıl çalışıyor model
	-> hiç görmediği türlerde nasıl çalışıyor model
	-> modelin genellendirmesi hakkında bir fikir sahibi olmuş oluyoruz


Gerçek casete mesela fps yüksek ihtimal düşecek. O yüzden kendi deneylerinde hedef fps ten daha yükseğini hedeflemelisin

Bazı türleri çok iyi öğrenememiş olabilir -> daha fazla data toplaman lazım
Ya da kediye overfit edebilir -> data sayısı balance lanmalı vs

Modelin nasıl iyileştirileceğine dair intuition kazanma 

## Deployment 
Deep stream Nvidia versiyonuna dönüşüm
TensorRT versiyouna dönüşüm


## After Deployment - Monitoring
Continual Learning
Userlar environemnt değiştirebilir
Edge device'ın değişimleri bildirmesi lazım
	Kamera bozlması, çamr gelmesi vs
Hata için bildirim göndermesi lazım
Çok aşırı yağmurlu bir case'te sınfılandırma yapma diyebilirsin mesela
Elle threshold koyulabilir

Modelin loglarına bakarak model performansını sürekli takip etmeliyiz.
Modeli tekrar eğitmek gerekebilir
	Best practice: Son 3 ayda toplanan datayı kullanarak tekrar eğitebilirsin ama içine geçmişteki datasetinden de veri eklemelisin