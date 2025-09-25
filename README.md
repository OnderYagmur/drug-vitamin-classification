# drug-vitamin-classification

#GİRİŞ
Bu proje, Akbank Bootcamp kapsamında bireysel olarak gerçekleştirdiğim derin öğrenme tabanlı bir görüntü sınıflandırma uygulamasıdır. Amaç, ilaç ve vitamin ürünlerini otomatik olarak tanıyıp sınıflandırmaktır.

Projede yaklaşık 10000 sentetik görselden oluşan 10 sınıflı bir veri seti kullanılmıştır. Eğitim ve doğrulama için veri artırma (data augmentation) teknikleri uygulanmıştır.

Model olarak MobileNetV2 önceden eğitilmiş CNN modeli transfer learning ile temel alınmış ve üzerine özel sınıflandırma katmanları eklenmiştir. Eğitim süreci RMSprop optimizasyonu ve categorical_crossentropy kaybı ile gerçekleştirilmiş, early_stopping ve checkpoint yöntemleri kullanılmıştır.

Modelin performansı doğruluk ve sınıflandırma raporlarıyla değerlendirilmiştir.
