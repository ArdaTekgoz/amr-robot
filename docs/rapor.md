# AMR Robot - Gelişen Proje Raporu

Yazar: Arda TEKGÖZ. Başlangıç: 12 Ekim 2026. Güncelleme: 13 Ekim 2026. Revizyon: 0.3. Belge türü: bitirme projesi düzeninde çalışma taslağı; kurumun biçim şartları henüz verilmedi.

## Özet

Bu proje, tek katlı bir iç mekânda diferansiyel sürüşlü mobil robotla harita oluşturmayı ve kayıtlı haritada kullanıcının seçtiği erişilebilir konuma otonom hareket etmeyi amaçlar. STM32 tabanlı tekerlek kontrolü ile ROS 2 tabanlı navigasyon katmanı ayrı geliştirilecek, sonra fiziksel sistemde birleştirilecektir. Simülasyon ve fiziksel robot kabulü ayrı deneylerle değerlendirilecektir. Henüz uygulama veya performans sonucu yoktur.

İlk fiziksel ara teslimat V0, telefon veya kumandayla kontrol edilebilen mobil platformdur. Ardından temel otonom işlevler V1'de geliştirilecektir. Proje kişisel yetkinlik kazanımı ve ileride TEKNOFEST Sanayide Robotik Teknolojiler yarışmasına teknik altyapı oluşturma amacı taşır. Yarışma şartnamesi henüz değerlendirilmemiştir.

## 1. Problem, amaç ve kapsam

İlk haritalamada operatör robotu gezdirecek; sensör verisinden harita oluşturulacaktır. Hedefe otonom hareket kayıtlı haritada gerçekleşecektir. Ortamı kendi kendine keşfetme sonraki sürüme bırakılmıştır. A/B istasyonları, seçilebilir hedef yeteneği için tekrarlı test noktalarıdır.

Arda'nın kendi problem tanımı altı maddelik kullanım senaryosuyla sunuldu ve [vizyon/kapsam kaydında](vizyon-ve-kapsam.md) anlamı korunarak düzenlendi. Uzun vadede farklı düz zeminli mekânlarda yeniden haritalama, harita arayüzünde base/target seçimi, hedefte bekleme ve dönüş, kapalı yolda alternatif rota, QR ile görev zinciri ve modüler görüntü işleme işlevleri hedeflenir. İlk fiziksel teslimatın asgari kabulü manuel mobil platformdur.

Kapsam ve ölçülebilir hedefler: [V0 gereksinimleri](gereksinimler-v0.md) ve [V1 gereksinimleri](gereksinimler-v1.md). Gerçek test mekânı henüz seçilmedi. Arda ilk CAD çiziminde 2 × 2 m kare alan, 40 × 40 cm robot ve iki alternatif yol belirledi. [Alan çizimi](test-alani.md) varsayımsal senaryo olarak kaydedildi; fiziksel ölçüm veya geçilebilirlik sonucu değildir. “Her ortama uyum” bütün ortamların doğrulandığı anlamına gelmez; zemin/geometri/sensör koşulları kabul deneyinde sınırlandırılacaktır.

## 2. Başlangıç durumu ve yöntem

Arda'nın beyanı: ROS 2 Docker üzerinden daha önce kurulmuştur; Python ve C/C++ kodlarını analiz etme, takip etme ve gerektiğinde düzenleme deneyimi vardır. ROS 2'yi öğrenmek istemektedir. STM32 Nucleo alımı planlanmaktadır; kart modeli ve diğer parçalar seçilmemiştir. Motor, enkoder, sürücü ve sensör mevcut değildir. Kurulumun sürümü ve çalışırlığı henüz doğrulanmamıştır.

Yöntem: ihtiyacı tanımlama, tasarım/hesap, Arda'nın uygulaması, beklenen-gerçek karşılaştırması, kanıt ve raporlama. Her deneyin ortamı SIM veya FİZ olarak etiketlenecek; başarısız denemeler de saklanacaktır. AI danışmanlık ve belge düzenleme desteği sağlayacaktır.

## 3. İlgili çalışmalar ve teknik kaynaklar

Başlangıç kaynağı: ../amr-rapor.pdf, 12 Ekim 2026, 19 sayfa. Yol haritası ve görevler incelendi. Teknik kaynaklar ilgili uygulama görevinde okunup sürüm ve erişim tarihiyle kaydedilecek. Başlangıç PDF'sindeki web kaynaklarının tamamı ayrıca doğrulanmadı; blok şeması incelemelerinde aşağıdaki üç resmî kaynak okundu.

- [Nav2 Jazzy - Mapping and Localization](https://docs.nav2.org/jazzy/configuration_and_development/first_time_robot_setup_guide/sensors/mapping_localization/), erişim 12 Ekim 2026: LaserScan tabanlı haritalama/konumlanma ve yardımcı range verisinin ayrımı.
- [SLAM Toolbox resmî deposu](https://github.com/SteveMacenski/slam_toolbox), erişim 12 Ekim 2026: LaserScan girişi. Bu kontrol kurulu ROS sürümünün doğrulandığı anlamına gelmez.
- [ROS 2 Control Jazzy - diff_drive_controller](https://control.ros.org/jazzy/doc/ros2_controllers/diff_drive_controller/doc/userdoc.html), erişim 12 Ekim 2026: komut zaman aşımı ve eskimiş komut kavramı; kontrolcü seçimi veya proje timeout değeri değildir.

Kaynak kayıt biçimi: başlık, üretici/yazar, sürüm, URL, erişim tarihi, projede desteklediği karar. Literatür değerlendirmesi henüz yapılmadı.

## 4. Gereksinimler ve sistem mimarisi

Üst düzey rol ayrımı: STM32 PWM, enkoder okuma, sabit periyotlu hız kontrolü ve komut zaman aşımını; ROS 2 bilgisayarı odometri, TF, SLAM, konumlanma, navigasyon ve görev yönetimini üstlenecek. Motor sürücü, kontrol sinyalini motor gücüne aktaracak. Ayrıntılı arayüz henüz tasarlanmadı.

Arda'nın V01, V02 ve V03 [blok şemaları ve incelemesi](sistem-mimarisi-inceleme.md) kaydedildi. Gamepad/ROS 2 PC/STM32 yolu, iki sürücü-motor-enkoder grubu ve dört mesafe sensörü aday mimari olarak gösterildi. V02'de STM32-sürücü kontrol yönleri, PC komut/telemetri etiketleri ve renkli güç dağıtımı iyileştirildi; ayrı haritalama aygıtı eklendi. V03'te haritalama verisi PC'ye yönlendirildi, sürücü-motor enerji oku ve sol ön sensör ölçüm rengi düzeltildi. Motor-enkoder mekanik etiketi, enkoder besleme ihtiyacı ve harici laptop yerleşimine uygun güç/haberleşme notları açık. Dört köşe sensörü haritalama sensörü yerine kabul edilmedi.

Arda komut kesildiğinde durma sorumluluğunu STM32'ye verdi ve bağlantı bayrağına dayalı sözde kod önerdi. Danışman, bağlantı açık kalırken de komutun kesilebileceğini ve son geçerli komuttan beri geçen sürenin STM32'de izlenmesi gerektiğini açıkladı. Timeout eşiği, tekrar başlatma davranışı ve fiziksel duruş süresi henüz seçilmedi veya denenmedi. Yazılımsal komut timeout'u, fiziksel motor enerjisi kesme yolundan ayrı tutulur.

13 Ekim'de Arda son komut zamanını komut tamamlanınca güncellemeyi ve komut bitince durmayı önerdi. Bu cevapta görev tamamlanması ile sürekli hız komutu akışı karışmıştır. Danışman, kabul edilen her geçerli/güncel hız komutunun alınma anında zamanın yenilenmesini; komutlar kesildiğinde görevin bitmesi beklenmeden süreyle duruşun tetiklenmesini açıkladı. Arda zaman çizelgesi alıştırmasında 250/450 ms timeout durumlarını doğru yorumladı; son geçerli komut zamanı sorusuna cevap vermedi, 100 ms değeri danışman tarafından açıklandı. Bu alıştırma gerçek deney veya proje timeout değeri değildir.

Arda tek hedef isteğinin STM32'de rota planlanıp yürütülmesi gerektiğini sordu. Danışman seçilen görev ayrımını açıkladı: hedef ROS 2/Nav2'ye, rota/yol takibi ROS tarafına, güncel hız referanslarının tekerlek kontrolü ve timeout'u STM32'ye aittir. Tek görev birçok hız komutuyla yürütülür. [NavigateToPose](https://docs.nav2.org/jazzy/configuration_and_development/configuration_guide/core_servers/bt_plugins/actions/NavigateToPose/) ve [Controller plugin](https://docs.nav2.org/jazzy/tutorials/plugin_tutorials/writing_new_controller_plugin/writing_new_controller_plugin/) resmî açıklamaları 13 Ekim 2026'da bu ayrım için kontrol edildi. Arda'nın kısa kişisel rol özeti ve tüm üç akış kabulü henüz açık.

Kullanıcı ROS 2 PC'nin kendi laptopu olması ve robotla kablosuz bağlantı kurması beklentisini belirtti. Harici laptop başlangıç adayı olarak desteklendi. Robot tarafında kablosuz haberleşme birimi/arayüz, Nucleo bağlantısı ve V1 sensör verisini laptopa taşıma yolu seçilecek. Laptop kendi bataryası/adaptörüyle, robot üstündeki bileşenler robot güç dağıtımıyla beslenecek. Bu yerleşim henüz donanım/protokol seçimi veya kablosuz test sonucu değildir.

### Karar kaydı

| Tarih | Karar | Gerekçe / kaynak | Durum |
| --- | --- | --- | --- |
| 2026-10-12 | İlk harita operatör eşliğinde; otonom keşif sonraki sürüm | Kullanıcının açık seçimi; temel haritalama ve navigasyonu önce öğrenmek | Kapsam kararı |
| 2026-10-12 | Seçilebilir erişilebilir hedef; A/B kabul deneyi | Kullanıcının kullanım amacı ve kaynak raporun tekrarlı deneyi | Kapsam kararı |
| 2026-10-12 | Test alanı seçilmedi | Kullanıcının beyanı; ölçüm verisi yok | Açık konu |
| 2026-10-12 | V0 manuel mobil platform ilk fiziksel ara teslimat | Arda'nın kullanım senaryosu, madde 6 | Kapsam kararı |
| 2026-10-12 | V1 temel otonom hedef; QR, periyodik görev ve görüntü işleme sonraki sürüm | Arda'nın aşamalı geliştirme amacı; danışmanın kapsam düzenlemesi | Yol haritasına işlendi |
| 2026-10-12 | Geçilebilir alternatif yol ile tamamen kapalı yol ayrı deneyler | Yeniden planlamanın hedefe erişimi garanti etmemesi | Sayısal sınırlar bekleniyor |
| 2026-10-12 | Telefon veya kumandadan tek kontrol arayüzü V0 için yeterli | Arda'nın asgari prototip tanımı | Arayüz seçimi açık |
| 2026-10-12 | İlk varsayımsal alan 2 × 2 m; robot 40 × 40 cm; iki rota fikri | Arda'nın CAD çizimi ve açıklaması | Tasarım varsayımı; geçilebilirlik doğrulanmadı |
| 2026-10-12 | V02'de istasyon/engel etiketleri; 250 mm merkez-yüzey açıklıkları | Arda'nın revize CAD çizimi | Düz duruşta nominal gövde açıklığı 50 mm; dönüş doğrulaması sonraki görevlerde |
| 2026-10-12 | Gamepad/ROS 2 PC/STM32 yolu ve dört köşe sensörü aday mimari | Arda'nın ilk sistem blok şeması | Akış revizyonu ve sensör işlevlerinin ayrımı bekleniyor; parça seçimi değil |
| 2026-10-12 | Komut kesilmesinde durma kararının STM32'de olması | Arda'nın kişisel açıklaması | Son geçerli komut yaşını izleme kuralı ve eşik henüz tamamlanmadı |
| 2026-10-13 | Harici laptop ve kablosuz robot bağlantısı başlangıç adayı | Arda'nın kullanım beklentisi ve danışman açıklaması | Haberleşme birimi, protokol ve sensör veri yolu seçilecek |

İlk sayısal hedefler Arda tarafından gerekçelendirildi: nominal seyir 0,25–0,35 m/s (dar alanda hızlanma/yavaşlama alanı), boş yükte geniş alanda azami 0,45 m/s; hedef faydalı yük 5 kg, bütçe/motor uyumunda gerekçeli 3 kg revizyonu mümkün. Robot kendi kütlesi faydalı yükten ayrı hesaplanacak. Kullanıcı en az 30 dakika çalışma koşulunu 5 kg yükle nominal gidiş-dönüş çevrimi ve ilgili robot sensörleri açık olarak seçti; çevrim ayrıntısı henüz yazılmadı. Bu değerler ölçülen performans değildir.

12 V motorlar adaydır; pil kimyası/kapasitesi ve lojik/sensör beslemeleri seçilmedi. Kablolu manuel şarj beklentisi var; şarj süresi üst sınırı açık. Motor boyutlama ve güç bütçesi AMR-12'de yapılacak. İlk alanın geometri/duruş yeterliliği, nominal hız gerekçesiyle kendiliğinden doğrulanmış sayılmaz.

13 Ekim danışman örneğinde 0,45 m/s × 0,3 s = 0,135 m, frenleme başlamadan komut timeout'u beklemesindeki ideal sabit hızlı ilerlemedir. Proje timeout'u henüz seçilmedi. Tepki gecikmesi, frenleme ve açıklık marjının birlikte değerlendirilmesi [Nav2 rehberinden](https://docs.nav2.org/rolling/tutorials/general_tutorials/using_collision_monitor/using_collision_monitor/) kontrol edildi. Pil enerji hesabının güç-zaman ve V/Ah/Wh ilişkisi [TI SLVA642B bölüm 4.1](https://www.ti.com/lit/slva642) ile desteklendi; örnek bisiklet bileşenleri AMR için seçilmedi. Kalan tolerans/timeout/kabul eşikleri açık.

Arda ayrıca gamepad ile LiDAR haritalama, arayüzde hedef seçimi, “Nav2/A*/SLAM” ile rota hesabı, motor sürücü/enkoder kontrolü ve yeni engelde durmayı içeren uçtan uca kişisel senaryosunu sundu. Danışman SLAM'in harita/poz tahmini, Nav2 planlayıcısının rota, kontrolcüsünün güncel hız komutu üretimi görevlerini ayırdı; STM32'ye rota yerine hız referansları gönderileceğini ve enkoderin hareketi başlatmak yerine geri besleme sağladığını açıkladı. A* olası planlama algoritmasıdır; eklenti seçimi henüz yapılmadı. [Nav2 resmî açıklaması](https://docs.nav2.org/jazzy/configuration_and_development/first_time_robot_setup_guide/navigation_plugins/setup_navigation_plugins/) 13 Ekim 2026'da kontrol edildi.

Ses/LED komut-hareket-hedef bildirimleri ve algılanan yakın engelde yerel durma, R-13/R-14 olarak V1 gereksinim taslağına eklendi. Algılama eşiği/kapsaması, duruş ve yeniden başlama kuralı ile bildirim desenleri henüz belirlenmedi. LiDAR'ın en ucuz yöntem olduğu iddiası doğrulanmadı; model/arayüz/sürücü/bütçe AMR-12'de değerlendirilecek. V0'nun asgari manuel kapsamı bu yeni V1 işlevleriyle genişletilmedi.

## 5. Tasarım ve uygulama

Kinematik ve birimler (AMR-04): başlanmadı.

ROS düğümleri, model ve simülasyon (AMR-02–11): önceki Docker kurulumu bildirildi; proje uygulaması ve kabulü yapılmadı.

Donanım boyutlama, bütçe ve STM32 kontrolü (AMR-12–19): başlanmadı.

Şasi, güç, kalibrasyon ve gerçek navigasyon (AMR-20–23): başlanmadı.

Her bölümde tasarım gerekçesi, kendi geliştirilen parça, kullanılan hazır bileşen ve sınırları, hata ve düzeltme bulunacak.

## 6. Deney tasarımı ve sonuçlar

Şu anda ölçülen sonuç yoktur. Kabul deneyinden önce eşikler ve tekrar sayısı dondurulacak. SIM referansı ile FİZ ölçüm yöntemi ayrı tanımlanacak; robotun kendi tahmini, bağımsız fiziksel gerçek ölçümün yerine geçmeyecek.

| Deney ID | Gereksinim | SIM/FİZ | Koşullar | Beklenen | Ölçülen | Geçti/kaldı | Kanıt |
| --- | --- | --- | --- | --- | --- | --- | --- |

## 7. Tartışma, sınırlamalar ve gelecek çalışmalar

Başlangıç sınırlamaları: donanım, test alanı, ilk kontrol arayüzü ve sayısal hedefler eksik. Simülasyonun fiziksel sisteme aktarımı henüz incelenmedi. Otonom keşif, QR, periyodik görev ve üst modül ayrı sonraki kapsamlardır; ek süre tahmini yapılmadı. Yarışma şartlarına uygunluk değerlendirilmedi.

Sonuçlara dayalı değerlendirme: deneylerden sonra yazılacak.

## 8. Sonuç

Henüz proje sonucu yoktur. Bu bölüm ancak ölçülmüş sonuçlar ve gereksinim değerlendirmesiyle tamamlanacak.

## 9. Kişisel katkı ve öğrenme

Arda: kullanım hedefini, başlangıç deneyimini/donanım durumunu ve ilk haritalama yöntemini açıkladı; altı maddelik senaryosunda kişisel gelişim/yarışma altyapısı amacını, modüler robot vizyonunu ve manuel ilk prototip beklentisini belirledi. 2 × 2 m alan ve 40 × 40 cm robot varsayımıyla iki alternatif rota içeren ilk CAD çizimini oluşturdu. İlk sistem blok şemasını da çizdi; bu şemanın revizyonu ve kişisel akış açıklamaları, sayısal performans gereksinimleri ve robot uygulaması henüz bekleniyor.

Arda ayrıca V02 çiziminde BASE / ROBOT, TARGET ROBOT ve ENGEL etiketleri ile yol merkezi açıklıklarını ekledi. Bu çizim alan tanımı kanıtıdır. Dönüşlerde kare gövdenin kapladığı alanın kontrolü ve rotaların uygulanması henüz yapılmadı.

Blok şemasının V02 revizyonunda renk anahtarı, kontrol yönleri, PC komut/telemetri etiketleri, güç dalları ve haritalama bloğunu ekledi. Komut kaybında STM32'nin durmayı yönetmesi gerektiğini kendi sözleriyle belirtti; zaman aşımının tespit yöntemi henüz revize edilecek.

13 Ekim'de V03 revizyonunu sundu ve motor sürücü/enkoderin temel görevlerini kendi sözleriyle ayırdı. Son komut zamanı ve duruş anı açıklamalarındaki görev/komut ayrımı eksikliği ile laptop/kablosuz bağlantı sorusu [13 Ekim oturumunda](oturumlar/2026-10-13-AMR-01.md) gerçek yanıtlarıyla kaydedildi. Eksik öğrenme sonucu tamamlandı diye işaretlenmedi.

AI: mevcut raporu inceledi; depo, yol haritası, çalışma sayfaları ve rapor iskeletini hazırladı. Bu hazırlık Arda'nın teknik uygulama kanıtı değildir.

Her görevde Arda'nın kendi açıklaması ve öğrendiği konu [oturum kaydında](oturumlar/2026-10-12-AMR-01.md) tutulacak.

## Ekler

- [Yol haritası](yol-haritasi.md)
- [AMR-01 çalışma yönergesi](gorevler/AMR-01.md)
- [Kanıt kayıt düzeni](../evidence/README.md)
- İleride: BOM, bağlantı şeması, protokol, hesaplar, deney CSV'leri, kurulum ve demo.
