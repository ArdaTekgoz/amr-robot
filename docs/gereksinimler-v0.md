# V0 - Manuel mobil platform gereksinimleri

Revizyon: 0.2 taslak | Güncelleme: 13 Ekim 2026 | Durum: ilk hız/yük/süre hedefleri kaydedildi; kalan eşikler ve donanım doğrulaması bekleniyor.

İlk fiziksel prototip: düz zeminde operatörün telefon veya kumanda üzerinden hareket ettirebildiği diferansiyel sürüşlü platform. Bu teslimat, otonom AMR geliştirmesinin hareket tabanıdır.

İlk [varsayımsal alan çiziminde](test-alani.md) alan 2 × 2 m, robot gövdesi 40 × 40 cm olarak kabul edildi. Bunlar geçici tasarım varsayımlarıdır; nihai şasi/parça seçimi değildir.

| ID | Gereksinim | Doğrulama |
| --- | --- | --- |
| V0-01 | Seçilecek tek arayüzden ileri, geri, sağ/sol dönüş ve durma komutları | Tanımlı test alanında her komut için beklenen/gerçek hareket kaydı |
| V0-02 | Komut bırakılınca belirlenen davranışla durma; başlangıç/reset sonrasında istemsiz hareket olmaması | Başlangıç, reset ve komut bırakma deneyi; davranış/süre seçilecek |
| V0-03 | Başlangıç danışman varsayımı: güncel komut 20 Hz; son geçerli komuttan ≥250 ms sonra ilk STM32 kontrol çevriminde sıfır tekerlek referansları | Bağlantı kesme: son geçerli mesaj, eşik, kontrol çevrimi gecikmesi, sıfır referans ve gerçek duruş sürelerini ayrı ölç. AMR-17/18'de doğrulanacak/revize edilecek |
| V0-04 | Nominal seyir 0,25–0,35 m/s; boş yükte geniş alanda azami 0,45 m/s; açısal sınır henüz seçilmedi | Referans/ölçülen hız logu. Nominal bant ve boş yük azami koşulunu ayrı dene; dar alan hızını duruş/açıklık ölçümlerine göre sınırla |
| V0-05 | 5 kg hedef faydalı yükle, nominal hız bandında tanımlı gidiş-dönüş çevrimi ve ilgili robot sensörleri açıkken en az 30 dakika | Yük, rota, hareket/bekleme oranı, elektronik konfigürasyonu ve robot batarya enerji/süre kaydı. Çevrim ayrıntısı henüz yazılacak |
| V0-06 | Motor enerjisini fiziksel olarak kesebilme; kablo/güç düzeninin doğrulanması | AMR-20 güç kontrolü ve enerjiyi kesme deneyi |
| V0-07 | Ölçülen tekerlek kontrolü ve odometri kalibrasyonu | AMR-19 ve AMR-21 sonuçları; otonom navigasyon gerektirmez |

Başlangıç kontrol tercihi gamepad'dir. Modeli/haberleşme yöntemi, açısal hız, fiziksel duruş eşiği ve tekrar sayısı henüz seçilmedi. İlk doğrusal hız/yük/süre hedefleri Arda tarafından gerekçelendirildi. 20 Hz/250 ms timeout danışman başlangıç varsayımıdır; kullanıcı ölçümü veya resmî varsayılan diye sunulmaz. Donanımda hiçbir hedef denenmedi. Fiziksel duruş sınırı AMR-12'de motor/sürücü kararıyla, komut/çıkış davranışı AMR-17/18'de doğrulanacak. V0-07 öğrenme hedefleriyle mevcut görev bağımlılıklarını korur. Gereksinimler ölçülmeden V0 tamamlandı denmez.

5 kg robotun kendi kütlesinden ayrı faydalı yüktür. Kullanıcı fiyat/performans motor seçimi gerektirirse 3 kg'a düşürmeyi kabul edebileceğini belirtti. Şimdiki hedef 5 kg'dır; AMR-12'de 3 kg seçilirse gereksinim gerekçeli revize edilir ve 3 kg sonucu 5 kg başarısı olarak sunulmaz. Nominal hız bandının 5 kg yükle uygulanabilirliği hesap/ölçümle kontrol edilecek.

12 V motorlar aday güç mimarisidir; motor modeli/pil/kapasite/kimya seçilmedi. Lojik, sensör ve enkoder beslemeleri seçilen parçaların veri sayfalarına göre dağıtılacak. Laptop kendi beslemesini kullanır. Kablolu manuel şarj beklentisi kaydedildi; şarj süresi için sayısal üst sınır henüz belirlenmedi. Bunlar AMR-12/20'de kesinleştirilecek.

Arda'nın [ilk blok şemasında](sistem-mimarisi-inceleme.md) gamepad → ROS 2 PC → STM32 manuel kontrol yolu önerildi. Bu aday mimaridir; bilgisayar yerleşimi ve bağlantı yöntemleri seçilmedi. Dört köşe mesafe sensörü V0'nun asgari kabulüne zorunlu özellik olarak eklenmedi.

13 Ekim senaryo açıklamasında Arda ilk gezdirme/haritalama için gamepad kullanımını tercih etti. İlk kontrol yaklaşımı gamepad olarak kayıtlı; model ve USB/Bluetooth bağlantısı seçilmedi. Telefon arayüzü başlangıç için ayrıca zorunlu değildir.

13 Ekim güncellemesi: Arda ROS 2 PC'nin kendi laptopu olmasını ve robotla kablosuz haberleşmesini beklediğini belirtti. Harici laptop başlangıç adayı olarak desteklendi; robot tarafı kablosuz birim ve protokol henüz seçilmedi. Laptop kendi beslemesiyle, robot bileşenleri robot güç dağıtımıyla beslenecek. Laptopun Docker/ağ çalışırlığı ve kablosuz veri yolu henüz doğrulanmadı.

V0 dışı: harita, otonom rota, otomatik engelden kaçınma, QR, görüntü işleme, görev zamanlama ve üretilmiş üst modül. Modülerliğe yönelik mekanik paylar AMR-12/20'de planlanacak.
