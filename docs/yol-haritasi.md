# Yol haritası

Kaynak: kökteki amr-rapor.pdf, 12 Ekim 2026. Bu belge kaynak planı takip eder; aşağıdaki görevler uygulama kanıtı değildir.

Ana kapsam 204 saat; haftada 6 saat ile yaklaşık 34 çalışma haftası, %25 planlama payıyla yaklaşık 43 hafta. Tedarik ve diğer beklemeler dahil değildir. Sonraki sürümler ayrıca 58 saattir. Tahminler teslim tarihi taahhüdü değildir.

## Kullanıcıyla netleşen kapsam

12 Ekim 2026: İlk harita operatörün robotu gezdirmesiyle oluşturulacak. Kayıtlı haritada kullanıcının seçtiği erişilebilir hedefe otonom navigasyon geliştirilecek. A/B istasyonları sabit kabul deneyi olarak kullanılacak. Otonom keşif sonraki sürüme bırakıldı; kaynak rapordaki 29 göreve dahil değil, ayrıca tahmin edilecek.

## Görevler ve ön koşullar

| Görev | İş | Ön koşul | Tahmin (saat) | Durum |
| --- | --- | --- | ---: | --- |
| AMR-01 | Görev tanımı ve sistem sınırları | Başlangıç | 4 | Devam ediyor |
| AMR-02 | ROS 2 ve Gazebo ortamı | 01 | 8 | Başlanmadı |
| AMR-03 | Kendi ROS düğümü | 02 | 8 | Başlanmadı |
| AMR-04 | Diferansiyel sürüş hesabı | 03 | 6 | Başlanmadı |
| AMR-05 | Robot modeli | 04 | 8 | Başlanmadı |
| AMR-06 | Hız komutu ve simülasyon köprüsü | 05 | 8 | Başlanmadı |
| AMR-07 | Odometri ve TF | 06 | 8 | Başlanmadı |
| AMR-08 | Mesafe sensörü ve haritalama | 07 | 8 | Başlanmadı |
| AMR-09 | Kayıtlı haritada konumlanma | 08 | 10 | Başlanmadı |
| AMR-10 | Nav2 hedef ve maliyet haritaları | 09 | 8 | Başlanmadı |
| AMR-11 | Simülasyon v1 kabulü | 10 | 8 | Başlanmadı |
| AMR-12 | Donanım seçimi ve bütçe | 01 | 8 | Başlanmadı |
| AMR-13 | STM32 ilk uygulama ve debug | 12 | 8 | Başlanmadı |
| AMR-14 | PWM ve motor sürücü | 13 | 8 | Başlanmadı |
| AMR-15 | Enkoder ve hız ölçümü | 14 | 10 | Başlanmadı |
| AMR-16 | Ölçülen PI/PID hız kontrolü | 15 | 10 | Başlanmadı |
| AMR-17 | İki motor ve komut zaman aşımı | 16 | 10 | Başlanmadı |
| AMR-18 | STM32-ROS haberleşmesi | 17, 03 | 10 | Başlanmadı |
| AMR-19 | Kendi tekerlek odometrisi | 18, 04 | 8 | Başlanmadı |
| AMR-20 | Şasi ve güç sistemi | 12, 19 | 10 | Başlanmadı |
| AMR-21 | Teleop ve fiziksel kalibrasyon | 20 | 10 | Başlanmadı |
| AMR-22 | Gerçek sensör ve harita | 21, 08 | 10 | Başlanmadı |
| AMR-23 | Fiziksel navigasyon | 22, 10 | 10 | Başlanmadı |
| AMR-24 | Fiziksel v1 kabulü | 23, 11 | 8 | Başlanmadı |
| AMR-25 | Falstad devre incelemesi | 24 | 6 | Sonraki sürüm |
| AMR-26 | Altium ara kartı | 25 | 16 | Sonraki sürüm |
| AMR-27 | OpenCV istasyon işareti | 24 | 14 | Sonraki sürüm |
| AMR-28 | YOLO nesne algılama | 27 | 12 | Sonraki sürüm |
| AMR-29 | Ollama sınırlı görev arayüzü | 24 | 10 | Sonraki sürüm |

01 tamamlanınca ortam kolu (02) ve donanım bütçesi kolu (12) açılır. Donanım alımı, simülasyon v1'in bitmesini beklemek zorunda değildir; donanım beklenirse simülasyonda ön koşulu uygun göreve geçilir.

## Kabul kapıları

- AMR-01: Bir sayfalık kapsam, gerekçeli geçici performans değerleri ve Arda'nın kendi blok şeması; üç akışı kendi sözleriyle açıklaması.
- AMR-12: İlk tezgâh için veri sayfası ve elektriksel/mekanik uyumla gerekçeli bütçe. Tam robot alımı ikinci dilimdir.
- AMR-11: On sabit simülasyon denemesinin tüm sonuçları ve AMR-01'de seçilen başarı eşiği. İptal ve ulaşılamaz hedef davranışı da incelenir.
- AMR-19: Gerçek kontrol, timeout, haberleşme ve odometri doğrulanmış olmalı; ardından fiziksel entegrasyon.
- AMR-24: On fiziksel görev ve bütün v1 gereksinimlerinin geçti/kaldı değerlendirmesi; temiz açılıştan tekrarlanabilir demo.

Simülasyon sonucu fiziksel sonuç yerine yazılmaz. Kabul eşiği deney sonucunu gördükten sonra başarıyı sağlamak için değiştirilmez; gerekçeli revizyon ayrı kaydedilir.
