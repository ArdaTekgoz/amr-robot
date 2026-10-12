# AMR v1 - Gereksinim çalışma sayfası

Revizyon: 0.1 taslak | 12 Ekim 2026 | Durum: Arda'nın kararları ve sayısal hedefleri bekleniyor.

## Amaç ve kapsam

Tek robot, tek katlı iç mekân, diferansiyel sürüş. Operatör robotu gezdirirken harita oluşturulur; kayıtlı haritada kullanıcının seçtiği erişilebilir hedefe otonom navigasyon yapılır. A/B noktaları tekrarlı kabul senaryosudur. Görev durumu ve hatalar bildirilir.

V1 dışı: otonom keşif, merdiven, dış mekân, otomatik yükleme/boşaltma, robot kolu/ArmPilot bütünleşmesi, filo yönetimi, endüstriyel sertifikasyon, özel PCB, kamera/YOLO/Ollama. Bunlar v1'in ölçülen başarı iddiasına dahil değildir.

## Çalışma ortamı

Gerçek mekân: seçilmedi. Alan, zemin, en dar geçiş, istasyon mesafesi ve robot boyutu: henüz belirlenmedi. Simülasyon ortamı varsayımları: Arda yazacak.

## Gereksinimler ve doğrulama

Boş alanlar eksik karardır; varsayılan başarı değeri değildir. SIM ve FİZ testleri ayrı kaydedilir.

| ID | Beklenen davranış / hedef | Durum | Doğrulama yöntemi |
| --- | --- | --- | --- |
| R-01 | Operatör gezdirirken harita oluşturup kaydetme; temiz oturumda yeniden yükleme | Kapsam kararı; denenmedi | SIM/FİZ: bilinen duvarlar ve yeniden açılış |
| R-02 | Kayıtlı haritada seçilen erişilebilir hedefe otonom gitme | Kapsam kararı; denenmedi | SIM/FİZ: sabit A/B görev dizisi |
| R-03 | İlerliyor, ulaştı, iptal edildi, başarısız durumlarının gözlenebilmesi | Tasarım hedefi; denenmedi | Normal görev, iptal ve ulaşılamaz hedef deneyi |
| R-04 | Azami doğrusal hız: ... m/s; açısal hız: ... rad/s | Geçici değer seçilecek | Referans/ölçülen hız logu; fiziksel hız kontrolü |
| R-05 | Faydalı yük: ... kg; robot kütlesinden ayrı | Geçici değer seçilecek | FİZ: tanımlı yük ve aynı rota deneyi |
| R-06 | Çalışma süresi: ... dakika; yük/hareket oranı: ... | Geçici değer seçilecek | FİZ: tanımlı çevrim ve enerji/çalışma kaydı |
| R-07 | Hedef konum hatası ≤ ... m; açı hatası ≤ ... derece | Geçici değer seçilecek | SIM: dünya referansı; FİZ: bağımsız konum/açı ölçümü |
| R-08 | SIM başarı: ... /10; FİZ başarı: ... /10 | Deneyden önce seçilecek | On sabit görev; başarısızlar dahil tam kayıt |
| R-09 | Geçerli komut kesilince timeout: ... ms; fiziksel duruş sınırı: ... s | Geçici değer seçilecek | Son geçerli mesaj, sıfır referans ve gerçek duruş zamanlarını ayrı ölç |
| R-10 | İptalde durma; ulaşılamaz hedefte tanımlı hata bildirimi | Süre/koşul seçilecek | SIM/FİZ: iptal ve kapalı yol senaryosu |

R-08'de “başarı” tanımı: doğru hedef + R-07 toleransı + tanımlı süre sınırı (... s) + iptal/hata gerektirmeyen normal tamamlanma. Süre ve deney koşulları Arda tarafından yazılacak. R-09 timeout ile mekanik duruş süresi aynı büyüklük değildir.

PDF'deki 0,15 m konum eşiği bir öneridir. Her sayısal seçim için gerekçe ve revizyon raporda tutulur; donanım hedefleri AMR-12'de, fiziksel tolerans AMR-23'te ölçüm kabiliyetiyle gözden geçirilir. Bu sayfa bugün robotun başarılı olduğunu iddia etmez.
