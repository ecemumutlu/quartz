


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



question ve contextleri 


şöyle bir task açalım
bu datayı nasıl utilize edebilriiz yeni data oluşturmadan önce bunu düşünelim
task aç board üzerinden git
new line lar ile context sayısını karşılaştır doğru olanları al.


ilk task -> daha sutructured bir dataset yaratmak
context key altında vs dictionary oluşturablirsin

squad formatına bakılabilir
dattaste converter
uymayanlar fazlaysa uymayanlara ne yapabilriz


~~jira boardunda belirle~~
~~deep learning specialization kursu Module modle gidelim learning altına subtask aç~~




base chunk önemli değil
query ile retrieved chunka bakıp related olup olmadığına bak

bu json dosyası verileriyle modellerle bir inference al karşılaştırma yap

cuda
aliaba nlp ne kadar hızlı çalışıyor bak
alibaba nlp için histogram çıkart
fine tune yap ali baba nlp tekrar inference al histogram vs de bak

llama sunumu için hazırlan #low 



todo
- [x] Cuda problemini çöz
- [x] alibaba nlp ne kadar hızlı çalışıyor bak
- [x] alibaba nlp histogram çıkart
- [x] alibaba nlp finetune yap ve tekrar inference alıp histogramını da çıkart
- [ ] llama sunumu için hazırlan
- [ ] Coursera dls week5 module3

