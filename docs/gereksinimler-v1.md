# AMR v1 - Gereksinim çalışma sayfası

Revizyon: 0.5 taslak | Güncelleme: 13 Ekim 2026 | Durum: ilk hedefler ve başarı eşikleri kaydedildi; timeout başlangıç varsayımı danışman önerisidir, son AMR-01 kontrolü açık. İlk fiziksel ara teslimat için [V0 gereksinimleri](gereksinimler-v0.md) kullanılır.

## Amaç ve kapsam

Tek robot, tek katlı ve düz zeminli iç mekân, diferansiyel sürüş. Operatör robotu gezdirirken harita oluşturulur; kayıtlı haritada kullanıcının seçtiği erişilebilir hedefe otonom navigasyon yapılır. A/B veya base/target noktaları tekrarlı kabul senaryosudur. Görev durumu ve hatalar bildirilir. Farklı mekânlarda yeniden haritalama uzun vadeli kullanım amacıdır; ilk doğrulama tanımlı bir ortamda yapılır.

V1 dışı: otonom keşif, QR ile görev zinciri, görüntüyle hedef tanıma, periyodik görev zamanlama, üretilmiş modüler üst yapı, merdiven, dış mekân, otomatik yükleme/boşaltma, robot kolu/ArmPilot bütünleşmesi, filo yönetimi, endüstriyel sertifikasyon, özel PCB, kamera/YOLO/Ollama. Bunlar v1'in ölçülen başarı iddiasına dahil değildir.

## Çalışma ortamı

Gerçek mekân: seçilmedi. İlk varsayımsal alan 2 × 2 m, robot gövdesi 40 × 40 cm ve zemin düz kabul edildi. Arda iki alternatif rota çizdi; V02'de istasyon/engel etiketleri ve yol merkezi-duvar/engel açıklıkları 250 mm olarak gösterildi. Eksenlere paralel gövdede nominal açıklık 50 mm; dönüşte yeterlilik henüz doğrulanmadı. [Alan kaydı](test-alani.md) mevcut. Operatör yeri ve merkez yolu notu netleştirilecek. Bu değerler donanım boyutlandırma kararı veya fiziksel ölçüm değildir.

## Gereksinimler ve doğrulama

Boş alanlar eksik karardır; varsayılan başarı değeri değildir. SIM ve FİZ testleri ayrı kaydedilir.

| ID | Beklenen davranış / hedef | Durum | Doğrulama yöntemi |
| --- | --- | --- | --- |
| R-01 | Operatör gezdirirken harita oluşturup kaydetme; temiz oturumda yeniden yükleme | Kapsam kararı; denenmedi | SIM/FİZ: bilinen duvarlar ve yeniden açılış |
| R-02 | Kayıtlı haritada seçilen erişilebilir hedefe otonom gitme | Kapsam kararı; denenmedi | SIM/FİZ: sabit A/B görev dizisi |
| R-03 | İlerliyor, ulaştı, iptal edildi, başarısız durumlarının gözlenebilmesi | Tasarım hedefi; denenmedi | Normal görev, iptal ve ulaşılamaz hedef deneyi |
| R-04 | Nominal doğrusal hız 0,25–0,35 m/s; boş yükte geniş alanda azami 0,45 m/s; açısal hız ... rad/s | Kullanıcının geçici doğrusal hedefi; açısal sınır/dar alan limiti açık | Referans/ölçülen hız logu; 5 kg nominal ve boş yük azami koşulları ayrı |
| R-05 | Hedef faydalı yük 5 kg; robot kütlesinden ayrı. Bütçe/motor uyumuna göre gerekçeli 3 kg revizyonu mümkün | Kullanıcının geçici hedefi; AMR-12'de doğrulanacak/revize edilecek | FİZ: geçerli gereksinim revizyonundaki yükle aynı rota; 3 kg deneyi 5 kg kabulü değildir |
| R-06 | En az 30 dakika; 5 kg hedef yük, nominal hız bandında tanımlı gidiş-dönüş çevrimi, ilgili robot sensörleri açık | Kullanıcı koşulu seçti; çevrim ve hareket/bekleme oranı ayrıntısı açık | FİZ: yük/rota/elektronik konfigürasyonu ile enerji ve çalışma kaydı; laptop kendi beslemesi ayrı |
| R-07 | Hedef merkezine konum hatası ≤ 0,05 m; yön hatası ≤ 5° | Kullanıcının başlangıç hedefi; konum hatası toplam yatay mesafe olarak tanımlandı. Bütçe/ölçümle 0,06–0,07 m revizyonu mümkün | SIM: dünya referansı; FİZ: bağımsız konum/açı ölçümü. Nav2'nin tahmini toleransı tek başına gerçek ölçüm değildir |
| R-08 | SIM: en az 8/10; FİZ: en az 6/10 başarılı normal görev | Kullanıcının başlangıç prototipi başarı eşiği | On sabit erişilebilir görev, aynı ölçütlerle ve başarısızlar dahil tam kayıt. İptal/komut kaybı/engel duruşu ayrı kabul deneyleri |
| R-09 | Başlangıç önerisi: 20 Hz güncel hız komutu; STM32 son geçerli komuttan ≥250 ms sonra ilk kontrol çevriminde iki tekerlek referansını sıfırlar | Danışman tasarım varsayımı; bağlantı gecikmesi ve duruş ölçümüyle AMR-17/18'de gözden geçirilecek. Fiziksel duruş sınırı AMR-12'de motor/sürücü kararıyla tanımlanacak | Son geçerli komut, eşik, sıfır referans zamanı ve gerçek duruşu ayrı ölç. Kontrol çevrimi ek gecikmesi ve eski/bozuk paketleri de dene |
| R-10 | İptalde durma; ulaşılamaz hedefte tanımlı hata bildirimi | Süre/koşul seçilecek | SIM/FİZ: iptal ve kapalı yol senaryosu |
| R-11 | Algılanan engelde geçilebilir alternatif rota varsa yeniden planlama; rota yoksa sınırlı deneme sonrası durum bildirimi | Süre/yeniden deneme/sensör sınırları seçilecek | SIM/FİZ: alternatif yol açık ve bütün yollar kapalı deneylerini ayrı uygula |
| R-12 | Harita arayüzünden base/target seçme; açık başlatmayla target'a gitme, ... s bekleme ve base'e dönme | Temel görev dizisi hedefi; ayrıntı seçilecek | SIM/FİZ: gidiş, bekleme, dönüş ve iptal kayıtları; otomatik periyodik başlatma dahil değil |
| R-13 | Yakın mesafe algılama tarafından algılanan, haritada önceden bulunmayan engelde yerel durma davranışı; geçerli hız isteğini engel durumunda geçersiz kılma | Kullanıcı talebi; algılama kapsaması, eşik, filtre, duruş ve tekrar hareket koşulu seçilecek | FİZ: sensör görüşünde yeni engel; algılama anı, sıfır referans, duruş süresi/mesafesi ve durum bildirimi. Rota alternatifi ayrı R-11 deneyi |
| R-14 | Komut kabulü, hareket ve hedefe varış için sesli ve LED durum bildirimi | Kullanıcı talebi; desen, zamanlama ve “komut” olayının görev/hız mesajı ayrımı henüz netleştirilecek | FİZ: tanımlı olay-durum tablosu, ses/LED gözlemi ve kayıt; hedefe varış ROS tarafında doğrulanacak |

R-08'de “başarı” tanımı: doğru hedef + R-07 konum/yön toleransı + tanımlı süre sınırı + müdahalesiz, çarpışmasız normal tamamlanma. Görev başına süre sınırı ve kesin rota/çevrim AMR-10/11'de sabit deneyden önce yazılacak. İptal/komut kaybı/yakın engelde durma için ayrı gereksinimler de geçmelidir; 8/10 veya 6/10 yalnız normal navigasyon görevlerinin oranıdır. R-09 timeout ile mekanik duruş süresi aynı büyüklük değildir.

PDF'deki 0,15 m konum önerisinin yerine kullanıcı 0,05 m hedefini seçti. Bir bütçe ile sağlanabileceği henüz doğrulanmadı. 0,06–0,07 m'ye geçiş gerekirse AMR-12/23'te gerekçe, revizyon tarihi ve yeni deney koşulları yazılır; eski başarısız deneyler yeni eşikle geriye dönük başarılı yapılmaz. Her sayısal seçim/revizyon raporda tutulur. Bu sayfa bugün robotun başarılı olduğunu iddia etmez.

Konum hatası tanımı: e = √((x - x_hedef)² + (y - y_hedef)²) ≤ 0,05 m. Bu tanım her eksende bağımsız ±5 cm'den farklıdır; ±5 cm ifadesi başlangıç çalışma tanımında hedef merkezinden toplam mesafe olarak yazıldı. Yön hatası en kısa açı farkıyla değerlendirilir. İlk çizimdeki 50 mm gövde-duvar açıklığı ile 50 mm hedef toleransı aynı şey değildir; hedef konumu/footprint AMR-05/10'da birlikte gözden geçirilecek.

Timeout başlangıç varsayımı: 20 Hz = 50 ms komut aralığı, 250 ms = beş nominal aralık. Kısa paket gecikmelerinin gereksiz durma yaratması ile eski hız referansının sürdürülmesi arasında ilk denge önerisidir; kablosuz gecikmeye dair ölçülmüş dağılım yoktur. Normal gamepad bırakma/iptalde sıfır komut gönderilir, timeout beklenmez. Tekrar tekrar eski hız verisinin iletilmesi güncel komut sayılmaz. Motor kontrolünün kendi çevrim frekansı bu 20 Hz'den ayrı, AMR-16'da seçilecek.

Hız gerekçesi: kullanıcı nominal bandı dar alanda hızlanma/yavaşlama alanı için, azami hızı boş yükle geniş alan için önerdi. Bu gerekçe henüz yeterli durma mesafesi veya geometrik geçilebilirliğin doğrulandığı anlamına gelmez. Hız, tepki gecikmesi, frenleme ve alan açıklığı birlikte değerlendirilecek. 2 × 2 m ilk varsayımsal alan, geniş alan azami hız deneyiyle aynı koşul değildir.

12 V motor kullanımı adaydır; tüm bileşenlerin 12 V ile besleneceği varsayılmadı. Pil seçimi ortalama güç, süre, tepe akımı, besleme dönüşümleri ve maliyetle AMR-12'de yapılacak. Manuel kablolu şarj beklentisi var; şarj süresi üst sınırı henüz açık.

13 Ekim açıklaması: gamepad ile ilk haritalama ve LiDAR kullanımı tercih olarak ifade edildi; LiDAR tür/modeli, uyum ve maliyet karşılaştırması AMR-12'de yapılacak. “En ucuz çözüm” henüz doğrulanmadı. R-13 sensörlerin bütün nesneleri algıladığı iddiası değildir; durma, algılama kapsamı ve eşikler içinde sınanacak. Yerel durma davranışı ile ROS tarafındaki yeniden planlama/yeniden başlama birbirinden ayrıdır. R-13/R-14 V1 davranışları olarak kaydedildi; V0'nun manuel asgari kapsamını kendiliğinden genişletmez. Ses/LED bileşenlerinin ek maliyet ve uygulama etkisi henüz tahmin edilmedi.
