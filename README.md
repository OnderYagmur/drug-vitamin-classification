# drug-vitamin-classification

# GİRİŞ

Bu proje, Akbank Bootcamp kapsamında bireysel olarak gerçekleştirdiğim derin öğrenme tabanlı bir görüntü sınıflandırma uygulamasıdır. Amaç, ilaç ve vitamin ürünlerini otomatik olarak tanıyıp sınıflandırmaktır.

Projede yaklaşık 10000 sentetik görselden oluşan 10 sınıflı bir veri seti kullanılmıştır. Eğitim ve doğrulama için veri artırma (data augmentation) teknikleri uygulanmıştır.

Model olarak MobileNetV2 önceden eğitilmiş CNN modeli transfer learning ile temel alınmış ve üzerine özel sınıflandırma katmanları eklenmiştir. Eğitim süreci RMSprop optimizasyonu ve categorical_crossentropy kaybı ile gerçekleştirilmiş, early_stopping ve checkpoint yöntemleri kullanılmıştır.

Modelin performansı doğruluk ve sınıflandırma raporlarıyla değerlendirilmiştir.

# Model Optimizasyonu ve Geliştirme Süreci: Overfitting ile Mücadele

   Projeye başladığım ilk aşamada, MobileNetV2 tabanlı bir model ile eğitim yaparken overfitting problemi ile karşılaştım. Eğitim verilerinde yüksek doğruluk elde edilirken, doğrulama verilerinde performans düşük kaldı. Eğitim kaybı ve doğrulama kaybı grafiklerinde bu ayrışma açıkça görülüyordu.

İlk Deneme Parametreleri

-> Model: MobileNetV2

->Optimizer: ADAM (0.0001)

->Epoch Sayısı: 10

->Batch Size: 64

->Dropout: 0.2

->Erken Durdurma: 5

->Aktivasyon: RELU

->Dense Katmanlar: İki adet 256 nöronlu katman

## Overfitting’i Azaltmak İçin Yapılan Değişiklikler
Overfitting’i gidermek amacıyla model ve eğitim sürecinde şu değişiklikler yapıldı:

Veri artırma teknikleri detaylandırıldı (rotasyon, zoom, shear, horizontal flip).

Dropout oranı %20’den %50’ye çıkarıldı.

Dense katmanlar sadeleştirilerek tek bir 128 nöronlu katman kullanıldı.

Learning rate scheduler eklendi (lr=0.0001, decay_steps=1000, decay_rate=0.9).

Sonuç: Overfitting büyük ölçüde azaldı, ancak genel doğruluk hâlâ istenilen seviyede değildi.

## Performansı Yükseltmek İçin Son Optimizasyonlar
Daha yüksek doğruluk elde etmek amacıyla aşağıdaki değişiklikler yapıldı:

Optimizer ADAM yerine RMSprop olarak değiştirildi.

Epoch sayısı 30’a çıkarıldı.

Aktivasyon fonksiyonu RELU yerine LeakyReLU olarak belirlendi.

Veri artırma işlemi daha da detaylandırıldı.

Sonuç: Bu son optimizasyonlarla model, hem overfitting’i önleyerek hem de doğruluk değerini artırarak başarılı bir sınıflandırma performansı gösterdi.

## Grafiklerin Kullanımı

## <img width="945" height="479" alt="image" src="https://github.com/user-attachments/assets/64fff572-a6ee-41a7-b86a-b068ad42dc5a" />  Grafik 1 : İlk Deneme için Overfitting var 


## <img width="945" height="393" alt="image" src="https://github.com/user-attachments/assets/d6d68c5c-94b0-4db0-b9ac-f59069d157b0" /> Grafik2 : Overfitting yok ama başarı ortalama


## <img width="548" height="225" alt="image" src="https://github.com/user-attachments/assets/40ed384d-fb19-4af1-9ea7-30533b2396a6" /> Grafik3 : En son aldığım grafik Overfitting yok ve başarı iyi




# METRİKLER

Projede modelin performansı birkaç farklı yöntemle değerlendirilmiştir:

### 1- Eğitim ve Doğrulama Doğruluğu (Accuracy)

Modelin eğitim ve doğrulama sırasında doğruluk değerleri epoch grafiğinde gösterilmiştir.

Eğitim sırasında doğruluk sürekli artmış ve erken durdurma (EarlyStopping) ile modelin en iyi doğrulukta durması sağlanmıştır.

### 2-Eğitim ve Doğrulama Kaybı (Loss)

Eğitim ve doğrulama kayıp değerleri grafiklerle görselleştirilmiş, modelin öğrenme sürecindeki iyileşmeler takip edilmiştir.

Overfitting durumunu önlemek için dropout ve veri artırma teknikleri uygulanmıştır.

### 3-Test Seti Performansı

Test setinde model, categorical_crossentropy kaybı ile değerlendirilmiş ve doğruluk (accuracy) metriği hesaplanmıştır.

### 4-Sınıflandırma Raporu

classification_report kullanılarak, her sınıf için precision, recall ve F1-score değerleri hesaplanmıştır.

Bu metrikler, modelin hangi sınıflarda daha başarılı olduğunu ve hangi sınıflarda iyileştirmeye ihtiyaç olduğunu anlamamızı sağlamaktadır.

### 5-Görsel İnceleme

Test setinden rastgele seçilen görüntüler için gerçek ve tahmin edilen sınıflar görselleştirilmiş, doğru ve yanlış tahminler renklerle belirtilmiştir.

Bu sayede modelin hatalı sınıflandırmaları hızlıca gözlemlenebilir ve yorumlanabilir.


# EKLER 
Projemde model, GPU destekli bir ortamda (Kaggle Notebook) eğitilmiş ve test edilmiştir. Bu sayede eğitim süresi önemli ölçüde kısaltılmıştır.

Projede ayrı bir kullanıcı arayüzü (UI) veya deployment script’i bulunmamaktadır. Model, doğrudan notebook üzerinden çalıştırılarak veri setindeki performansı gözlemlenebilir.


# Sonuç ve Gelecek Çalışmalar
Bu proje, ilaç ve vitamin ürünlerinin görüntülerini sınıflandırmak için başarılı bir derin öğrenme modeli ortaya koydu. Modelin doğruluk ve sınıflandırma performansı, test verisi üzerinde yüksek bir başarı gösterdi ve sentetik veri setleri üzerinde derin öğrenme uygulamalarına güzel bir örnek oluşturdu.

Gelecek çalışmalarda proje şu yönlerde geliştirilebilir:

Kullanıcı Arayüzü (UI): Flask ile interaktif bir arayüz ekleyerek kullanıcıların görsel yükleyip sınıflandırma yapabilmesi sağlanabilir.

Gerçek Zamanlı Veri İşleme: Kameradan veya canlı veri akışından gelen görsellerin anlık sınıflandırılması eklenebilir.

Veri Setini Genişletme: Daha fazla ve gerçek görüntüler eklenerek modelin genelleme yeteneği artırılabilir.

Model Optimizasyonu: Farklı CNN mimarileri, ensembıl yöntemler veya hiperparametre optimizasyonu ile model performansı iyileştirilebilir.

Mobil Uygulama Entegrasyonu: Kullanıcılar telefonlarından ürün fotoğraflarını çekip sınıflandırma yapabilir.

Otomatik Veri Toplama: Web scraping veya API’ler kullanılarak veri seti dinamik olarak güncellenebilir.

Etik ve Güvenlik Kontrolü: Modelin hatalı sınıflandırma durumlarını ve yanlış pozitif/negatifleri analiz ederek güvenli kullanım stratejisi geliştirmek.
