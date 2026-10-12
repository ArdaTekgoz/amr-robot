# AMR-01 - İlk sistem blok şeması incelemesi

Tarih: 12 Ekim 2026. Şemayı çizen: Arda. İnceleme ve açıklama desteği: AI. Durum: V02 revizyonu alındı; kalan akış düzeltmeleri ve kişisel açıklamalar bekleniyor. Bu belge bitmiş tasarım veya devre bağlantı şeması değildir.

![Arda'nın ilk blok şeması](../evidence/AMR-01/blok-semasi-v01.png)

![Arda'nın revize blok şeması](../evidence/AMR-01/blok-semasi-v02.png)

## V02 incelemesi ve Arda'nın açıklaması

Arda haberleşmeyi yeşil, gücü kırmızı ve sinyali mavi gösterdi. Gamepad okunu tek yöne çevirdi; STM32 → sürücü kontrol yönlerini düzeltti; ROS 2 ↔ STM32 komut ve telemetrisini ayrı etiketledi. Güç dağıtım dalları ve ayrı haritalama aygıtı bloğu eklendi. Bu iyileştirmeler kişisel tasarım katkısı olarak kaydedildi.

Arda'nın açıklaması: “ROS 2 Bilgisayarı komut göndermeyi keserse robotun durmasına stm32 verir. İf ros2connection = 0 emergencystop=1”. Bu sözde koddur; derlenmiş veya denenmiş firmware değildir. Durma kararının STM32'de olması doğru sorumluluk seçimi; bağlantı kaybının hangi ölçütle belirlendiği henüz açıklanmadı.

### Komut zaman aşımı için danışman açıklaması

Fiziksel bağlantı açık kalabilirken ROS süreci komut üretmeyi bırakabilir. Bu yüzden bağlantı durum bayrağı tek başına yeterli değildir. STM32, kendi zaman kaynağıyla son kabul edilen geçerli ve güncel komuttan beri geçen süreyi izlemelidir. Bu süre seçilecek eşiği aşınca iki tekerlek hız referansı sıfırlanır ve komut zaman aşımı durumu kaydedilir. Bozuk/eski paketler veya yalnızca bir bayt gelmesi bu süreyi sıfırlamamalıdır. Protokol, tekrar başlatma davranışı ve çıkış/duruş ayrıntıları AMR-17/18'de uygulanacaktır.

Bugünkü öğrenme çıktısı firmware yazmak değil, bu davranışı ölçülebilir gereksinime dönüştürmektir. Eşik henüz seçilmedi; sıfır referansın verildiği an ile motorun fiziksel olarak durduğu an ayrı ölçülecek. Arda'nın `emergencystop` adı burada yazılımsal timeout duruşunu ifade eder; fiziksel motor enerjisi kesme yolunun yerine geçmez.

ROS 2 Control Jazzy diff_drive_controller belgesinde de komut eskimesi için timeout ve otomatik durma açıklanır. Bu yalnız kavramsal referanstır; bu projede söz konusu kontrolcü seçilmiş veya STM32 tarafındaki koruma uygulanmış değildir. Belgedeki varsayılan süre proje için seçilmiş eşik sayılmaz.

### V02'de kalan düzeltmeler

| Bölüm | Düzeltme |
| --- | --- |
| Haritalama aygıtı → STM32 | Bu projenin planlanan haritalama akışında veri uygun arayüzle ROS 2 bilgisayarına ulaştırılmalı. Şemada haritalama veri okunu PC'ye yönelt; fiziksel arayüz/model sonra seçilecek. |
| Sürücü → motor mavi ok | Bu bağlantı motorun sürülen elektriksel enerjisidir; kırmızı göster. STM32 → sürücü PWM/yön kontrol sinyali mavi kalır. |
| Motor → enkoder mavi ok | Ölçülen mil/tekerlek dönüşü mekanik ilişkidir; “mekanik dönüş” diye etiketle veya ayrı kesikli çizgi kullan. Enkoder → STM32 ölçüm sinyali mavi kalır. |
| Sol ön sensör → STM32 kırmızı ok | Mesafe ölçümünü taşıyorsa mavi olmalı. Sensörün besleme girişi güç kaynağı/dağıtımından ayrıca kırmızı gösterilir. |
| PC ve enkoder beslemeleri | Bilgisayarın kendi beslemesi veya robot güç dağıtımı seçeneği gösterilmeli. Enkoder besleme ihtiyacı seçilecek tipe göre ayrıca değerlendirilmeli. Besleme gerilimi/parça henüz seçilmez. |
| Görevler ve veri adları | Blok görev cümleleri; PWM/yön, enkoder sayımı, mesafe ve tarama verisi gibi ok etiketleri tamamlanmalı. |

Köşe mesafe sensörleri yardımcı aday, haritalama aygıtı V1 bloğudur. Sensör modelleri, bilgisayar konumu ve bağlantı yöntemi henüz kesinleşmedi.

### Bir sonraki küçük uygulama

Arda, V02 üzerindeki kısa akış düzeltmelerini yapacak; ardından kendi sözleriyle son geçerli komut zamanını nasıl güncelleyeceğini ve komut kesildiğinde neyi kontrol edeceğini açıklayacak. Ayrıca motor sürücü ve enkoderin görevlerini birer cümle yazacak. Henüz kodlama veya fiziksel test yapılmayacak; sonra AMR-01'in sayısal hedefler adımına geçilecek.

Ek kaynak (erişim 12 Ekim 2026): [ROS 2 Control Jazzy - diff_drive_controller](https://control.ros.org/jazzy/doc/ros2_controllers/diff_drive_controller/doc/userdoc.html), command timeout ve eskimiş komut açıklaması.

## İlk taslak inceleme kaydı (V01)

## Arda'nın önerisi

Gamepad ile ROS 2 bilgisayarının, bilgisayar ile STM32 Nucleo'nun çift yönlü bağlantısı gösterildi. Sol/sağ sürücü, motor ve enkoderler; dört köşe mesafe sensörü; güç kaynağı yerleştirildi. Enkoder ve sensör okları STM32'ye yöneldi. Bileşenlerin görev açıklamaları ve okların taşıdığı veri/enerji henüz yazılmadı.

Gamepad + ROS 2 PC, ilk manuel kontrol için aday mimaridir. Gamepad modeli/bağlantısı, bilgisayarın harici veya robot üstünde olması, Nucleo modeli ve sensör türleri henüz seçilmedi. Dört sensör önerisi satın alma kararı veya V0 kabulüne eklenmiş zorunlu özellik değildir.

## İnceleme

| Şemadaki ilişki | Değerlendirme / öğrenme noktası |
| --- | --- |
| Gamepad ↔ ROS 2 PC | Sürüş için gerekli veri gamepad'den bilgisayara düğme/eksen durumudur. Ters okun taşıdığı bir işlev yoksa kaldırılabilir; USB/Bluetooth'un fiziksel çift yönlülüğü işlevsel sürüş akışından ayrıdır. |
| ROS 2 PC ↔ STM32 | İki yön anlamlıdır; ayrı oklarla bilgisayardan hız/durma komutu, STM32'den enkoder/hız/durum geri beslemesi etiketlenecek. |
| Sol/sağ sürücü → STM32 | Motor kontrol komutu için yön ters: STM32 → sürücü. Sürücü durum/hata çıkışı ayrıca seçilirse ters yönde ayrı bir ok eklenebilir. |
| Sol/sağ motor → STM32 | Temel sürüşte motor doğrudan STM32'nin kontrol çıkışına bağlanmaz. Sürücü → motor enerji aktarımı eksik. Ölçüm yolu enkoder → STM32 olarak gösterilir. |
| Enkoder → STM32 | Ölçüm yönü uygun. Enkoderin ilgili motor/tekerlek dönüşünü ölçtüğü mekanik ilişki de gösterilmeli; elektriksel besleme ayrı akıştır. |
| Köşe mesafe sensörleri → STM32 | Tür ve arayüz uyumuna bağlı bir ölçüm yolu adayı. STM32'de okunan mesafenin ROS 2'ye nasıl aktarılacağı ve hangi işlevde kullanılacağı henüz açıklanmadı. |
| Güç kaynağı → STM32 | Enerji dağıtımı eksik. Motor sürücülerine ve sensör/enkoder/lojik bileşenlerine uygun besleme yolları; bilgisayarın kendi beslemesi veya robot güç dağıtımıyla beslenmesi gösterilmeli. Gerilimler henüz seçilmeyecek. |

Kontrol sinyali ile motorun besleme enerjisi farklıdır. Sürücü hem kontrol sinyalini hem motor beslemesini alır; motor akımını sürücü üzerinden yönetir. Bu nedenle STM32, motor sürücü ve motor için tek tür ok kullanmak yanlış anlamaya açıktır.

## Haritalama sensörü ile yakın mesafe algısı

Şemadaki dört mesafe sensörünün türü belirtilmedi. Tek yönlü yakın mesafe ölçümleri kastediliyorsa, bunları doğrudan başlangıç planındaki 2D SLAM sensörünün yerine kabul etmiyoruz. Yakın engel algılama ile haritalama veri ihtiyacı ayrı değerlendirilecek.

Nav2'nin Jazzy haritalama/konumlanma rehberinde slam_toolbox ve AMCL için LaserScan verisi kullanılıyor; sonar/IR verisinin costmap'e katılması ayrı range katmanında açıklanıyor. Bu ayrımdan hareketle, köşe sensörleri yardımcı yakın mesafe algısı adayı; V1 haritalama için uygun tarama sensörü ise ayrı seçim konusu olarak tutulur. Sensörler tamamen kör noktaları kapatıyor veya her engeli algılıyor varsayılmadı.

V1 şemasına “haritalama sensörü - tür/model AMR-12'de seçilecek” bloğu eklenebilir; uygun arayüz üzerinden ROS 2 bilgisayarına veri sağlayacağı gösterilir. V0 için bu donanımı hemen almak veya çalıştırmak gerekmiyor.

Kaynaklar (erişim: 12 Ekim 2026):

- [Nav2 Jazzy - Mapping and Localization](https://docs.nav2.org/jazzy/configuration_and_development/first_time_robot_setup_guide/sensors/mapping_localization/): haritalama/konumlanma ve range katmanı ayrımı.
- [SLAM Toolbox resmî deposu](https://github.com/SteveMacenski/slam_toolbox): LaserScan girişinin tanımı. Kurulu dağıtımın sürümü bu oturumda doğrulanmadı.

## Arda'nın sonraki uygulaması

Mevcut şemayı düzelt; AI tarafından hazırlanmış yeni bir şema kopyalamak yerine kendi çizimini geliştir:

1. Komut, ölçüm/geri besleme ve enerjiyi üç renk veya çizgi biçimiyle ayır; bir açıklama kutusu ekle.
2. Motor sürücü ve motor yollarını düzelt; enkoderin ölçtüğü motorla ilişkisini göster.
3. PC-STM32 çift yönünü ayrı veri okları olarak etiketle. Gamepad ters oku kalacaksa işlevini yaz.
4. Besleme dallarını göster; model/gerilim seçimini boş bırak. Harici bilgisayar kullanımı düşünülüyorsa ayrı besleme olarak işaretle.
5. Köşe sensörlerini yardımcı aday, haritalama sensörünü V1 bloğu olarak ayır. V0'a zorunlu sensör kabulü ekleme.
6. Her bloğa bir cümle görev yaz. Özellikle STM32'nin periyodik motor kontrolü ve komut kaybında durma sorumluluğunu belirt.

Kendi sözlerinle açıklama: STM32 neden motor sürücüye ihtiyaç duyar? Enkoder nasıl geri besleme sağlar? ROS bilgisayarı mesaj göndermeyi bırakırsa hangi blok hangi davranışı uygulamalıdır? V02 ile durma sorumluluğu cevabı alındı; son geçerli komut süresi açıklaması ve diğer iki cevap henüz bekleniyor.
