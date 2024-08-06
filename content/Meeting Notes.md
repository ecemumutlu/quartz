


başka alanlarla kesişimlerini düşün


Drug -> dokümanlar üzerine bir chat ama train etmeden

**Çapraz disiplinler arasındaki teknikleri başka tarafa kaydırabilir miyiz?**

**Uğraştığınız problemler sizin için bir sınırlandırma olmamalı**



tdd -> test driven development

 - pytest fixtures kullanıyoruz
 - training için test yazabilrisin
 - pytest e bak
 - environment.yml ve conda hallet
 - environementı kru

llama1 llama2 llama3 neyi değiştirmişler baştan sonra highşightları vererek git
-top down bir approach güderek oku
- chatpdf, chatbot vs pdf leri atıp bakabilirisn



bi encoderda
 - t1 i bir berte veriyorum. t2 yi başka berte
cross encoderda
 - t1 ve t2 yi aynı berte veriyorum



30.07.2024
metric learning aşina ol

ilk etap:
 - toy küçük bir dataset belirle şimdilik. İlk çalışıp çalışmadığına bakalım yani. Sistemin çalıştığını görmek için şimdilik ingilzice eri seti bile bulabilrisin.

1. küçük bir dataseti bul
2. türkçe pretrain edilmiş model var mı bak. Performans metriklerine bak ve inference alıp gözlem yap. BertTurk vs var sanırım ama farklı modeller de eğitilmiş.
	1. https://huggingface.co/dbmdz/bert-base-turkish-cased
	2. vs. vs. bul araştır
	3. küçük modeller ulmaya çalılıyotuz hızlı olması için o yüzden llamaturk gibi bir şeyi almak mantıklı değil
	4. araştırmanın key pointlerini not et
3. pretrain'i devam ettir (fine tune etme)
4. türkçe modeli embeddinge contrastive learning ile 
	1. bunu repoya bakarak yap



Inference için: 
asıl amaç rag
bir tarafa paragraf. diğer tarafa o paragrafın cevaplayabileeceği bir soru.
birkaç tane related birkaç tane unrelated paragraf ekle. diğer tarafa da cevaplayabilceği bir soru. Aradaki similarity score u almaya çalış


command line dan çalıştırılabilecek bir şeyler yapabilrisin. 

Minik dataseti yap wikipedia gibi kullan. Inference al türkçe modelleri üzerinde



 Bi-encoder kullanalım
 query leri yazdım ama çok istediğim gibi dönmedi.
 soru sorduğumuzda yakın şeyler çıkmıyor ama bi-encoder + cross-encoder yapabilriz

beraber in progress done board u aktiff kullan
artık sub-task olarak açma
