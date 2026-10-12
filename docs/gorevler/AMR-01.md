# AMR-01 - Görev tanımı ve sistem sınırları

Tarih: 12 Ekim 2026. Tahmin: 4 saat. Gerçek süre: henüz kaydedilmedi. Durum: devam ediyor. Donanım gerekmez.

Son oturum: [13 Ekim 2026](../oturumlar/2026-10-13-AMR-01.md). Bu görev birkaç oturuma yayıldı; tamamlanma tarihinden bağımsız olarak kanıtla değerlendirilecek.

## Bugünün öğrenme hedefi

Bir robot fikrini kapsamı belirli, ölçülebilir ve doğrulanabilir gereksinimlere dönüştürmek. Bugün kod veya parça satın alımı gerekmiyor.

## 1. Kullanım senaryosu - Arda'nın yanıtı alındı (25 dakika ilk öneri)

Kendi sözlerinle 5-7 cümle yaz: Robot ne yapacak, harita nasıl oluşacak, hedefi kim verecek, hedefe varınca ne olacak, yol kapalıysa ne bildirecek, hangi işleri v1'de yapmayacak?

Arda altı maddelik yanıtını verdi. [Senaryo ve kapsam](../vizyon-ve-kapsam.md) rapora işlendi. İlk fiziksel prototip V0 manuel platform; otonom hedefler V1 ve sonraki sürümlere ayrıldı. Bu alt adımın çıktısı var; AMR-01 bütünü henüz tamamlanmadı.

**Neden:** Kullanım senaryosu belirsizse başarılı çalışan bir yazılım bile ihtiyacını karşılamayabilir.

Ölçülmüş mekân yok. Bunu gizleme. Simülasyon için hayalî bir oda tasarlayabilirsin; boyutları “simülasyon varsayımı” diye etiketle. Gerçek alan ölçümleri daha sonra gelecek.

## 2. Alan ve istasyon çizimi (35 dakika öneri)

**Çizim güncellendi:** Arda 2 × 2 m kare alan, varsayımsal 40 × 40 cm robot ve iki alternatif rota çizdi. V02'de base/target/engel etiketleri ve 250 mm yol merkezi açıklıkları var. [Çizim ve inceleme](../test-alani.md) kayıtlıdır. Eksenlere paralel sürüşte 50 mm nominal gövde açıklığı hesaplandı; dönüşte geçilebilirlik henüz doğrulanmadı. Alan tanımı bu görevde ilerlemek için yeterli; operatör yeri ve merkez yolu notu küçük belge eksikleridir.

Kâğıtta veya tercih ettiğin çizim aracında bir oda, duvarlar, sabit engel ve iki hedef noktası çiz. Eksen yönünü, metre cinsinden boyutları, en dar geçişi ve başlangıç noktasını işaretle. Ölçü yoksa varsayım yaz. A/B bu çizimde kabul deneyi için kullanılacak.

Şimdiki küçük görev: düz zeminli hayalî bir test alanı çiz; yaklaşık boyutlarını, robot başlangıcını, operatörün yerini, base ve target noktalarını, bir engeli ve çevresindeki boşluğu işaretle. “Varsayımsal test alanı” yaz. V0'da engeli operatör görecek ve yönetecek; çizimdeki otonom alternatif rota davranışı V1'e aittir. Boyutlar satın alma kararı değildir.

**Neden:** Robot boyutu ve geçiş genişliği, hangi hedeflerin erişilebilir olduğunu belirler. İlk çizim gerçek test alanı haritası değildir.

## 3. Sistem sınırı ve sorumluluklar (45 dakika öneri)

**Bu adımın ilk çıktıları alındı; aktif uygulama artık 4. adımdaki sayısal hedeflerdir.** Alan çizimi ve blok şeması kayıtlıdır. Kalan küçük akış/yerleşim notları son incelemede tamamlanacak. Henüz model, pin, gerilim veya haberleşme teknolojisi seçmek gerekmiyor.

**İlk şema alındı:** Arda gamepad, ROS 2 PC, Nucleo, sol/sağ sürücü-motor-enkoder, dört mesafe sensörü ve güç kaynağını çizdi. [Şema incelemesinde](../sistem-mimarisi-inceleme.md) motor kontrol okları, sürücü-motor bağlantısı, güç dalları ve veri etiketleri için düzeltmeler kayıtlı. Gamepad mimarisi ve dört sensör henüz aday; haritalama sensörü ayrı seçim konusu. Şimdiki küçük uygulama bu şemanın revizyonudur.

**V02 alındı:** Renk anahtarı, doğru STM32 → sürücü kontrol okları, ayrı PC komut/telemetri okları ve güç dalları eklendi. Arda komut kaybında durma sorumluluğunu STM32'ye verdi. Haritalama verisinin PC'ye yönlendirilmesi, sürücü-motor gücünün kırmızı gösterilmesi, mekanik enkoder ilişkisi, sol ön sensör veri oku ve besleme notları kalıyor. Kişisel açıklamada bağlantı bayrağından son geçerli komutun yaşına geçilecek; firmware henüz yazılmıyor.

**V03 alındı / 13 Ekim:** Haritalama-PC veri yolu, sürücü-motor güç rengi ve sol ön sensör ölçüm rengi düzeltildi. Motor sürücü/enkoder temel rol açıklamaları alındı. Komut tamamlanmasıyla komutun alınma zamanı karıştığından kısa zaman çizelgesi alıştırması yapılacak. Laptopun harici olması ve robotla kablosuz haberleşme beklentisi kaydedildi; arayüz seçimi açık. Önce bu kavram netleşecek, sonra geçici performans değerlerine geçilecek.

**Alıştırma yanıtı alındı:** Arda 250/450 ms timeout koşullarını doğru yorumladı. Son geçerli komutun 100 ms'de alındığı danışman tarafından açıklandı; Arda bu soruya cevap vermedi. Arayüzdeki tek hedef görevi ile STM32'ye giden güncel hız komutlarının ayrımı açıklandı: hedef/rota/takip ROS 2/Nav2'de, tekerlek kontrolü ve timeout STM32'de. Kişisel kısa rol özeti ve kalan yerleşim notlarıyla mimari adımı kapatılacak.

**Uçtan uca kişisel açıklama alındı:** Arda gamepad ile LiDAR haritalama, arayüz hedefi, navigasyon, sürücü/enkoder, yeni engelde durma ve ses/LED bildirimlerini anlattı. SLAM/planlama ayrımı, STM32'ye giden güncel hız referansı ve enkoder geri beslemesi için düzeltmeler açıklandı. Temel senaryo sayısal hedeflere geçmek için yeterli; bütün akışların kişisel açıklama kabulü son incelemede kalır. Yeni V1 davranışları R-13/R-14 olarak kaydedildi.

STM32, ROS 2 bilgisayarı, motor sürücü, motorlar, enkoderler, mesafe sensörü ve güç kaynağı için bloklar çiz. Her okun üzerine “ne taşınıyor?” yaz. Komut, geri besleme ve enerji için ayrı ok biçimi/renk seç.

Kendine sor: Hedef koordinatı ile motor sürme komutu aynı şey mi? Enkoder bana hangi ölçümü verir? Motor enerjisini hangi blok sağlar? Bilgisayardan mesaj gelmezse hangi blok karar vermeli?

**Neden:** Veriyi, kontrol kararını ve gücü ayırmak entegrasyon hatalarını bulmayı kolaylaştırır. Hazır şemayı kopyalamak yerine kendi şemanı açıklaman bekleniyor.

## 4. Gereksinimleri ölçülebilir yaz (50 dakika öneri)

[Çalışma sayfasını](../gereksinimler-v1.md) doldur. Hız, yük, çalışma süresi, konum/açı toleransı, başarı eşiği ve duruş davranışı için geçici hedef + gerekçe + ölçüm yöntemi yaz. Parça alımına bağlanan değerler AMR-12'de tekrar değerlendirilecek.

Önce [V0 çalışma sayfasındaki](../gereksinimler-v0.md) manuel kontrol hedeflerini seç; V1 konumlanma ve navigasyon hedeflerini ayrı tut. İlk kontrol tercihi gamepad; model ve bağlantı yöntemi açık.

Güncel tercih gamepad'dir; model/bağlantı seçimi AMR-12/18'de yapılacak. İlk küçük uygulama: düz sürüş için hedef hızı, robotun kendi ağırlığı dışında taşıyacağı faydalı yükü ve tanımlı kullanımda çalışma süresini Arda gerekçelendirecek. 2 m / seçilen süre hesabı hız birimini anlamak için kullanılabilir; gerçek rota uzunluğu 2 m sayılmaz.

**İlk üç hedef alındı:** nominal 0,25–0,35 m/s; boş yük/geniş alan azami 0,45 m/s; 5 kg hedef yük (AMR-12'de gerekçeli 3 kg revizyonu mümkün); en az 30 dakika, 5 kg nominal gidiş-dönüş çevriminde ilgili sensörler açık. Gerekçeler ve koşul [13 Ekim kaydında](../oturumlar/2026-10-13-AMR-01.md). 12 V motor/pil modeli henüz seçilmedi. Şimdi timeout/duruş, V1 toleransları ve başarı eşikleri kalan sayısal kararlardır.

Yazım kalıbı: “Robot, [tanımlı koşulda], [davranışı], [birim ve eşik] ile gerçekleştirmelidir; [deney yöntemi] ile doğrulanacaktır.”

Örnek: “Kayıtlı haritada, tanımlı boş rotada hedefe varma hatası en fazla ... m olmalıdır; ... referansına göre ölçülecektir.” PDF'deki 0,15 m yalnız ilk tasarım önerisidir; bugün seçilmiş veya ölçülmüş sonuç değildir.

## 5. İnceleme ve kişisel açıklama (35 dakika öneri)

Çizimini ve gereksinimlerini danışmana getir. Özellikle şu üç açıklamayı yardım almadan yapmayı dene:

1. Seçtiğim hedef, tekerlek hareketine nasıl dönüşüyor?
2. Robot hareketin gerçekleştiğini hangi geri beslemeyle anlıyor?
3. Güç kaynağından motor ve bilgisayara enerji nasıl gidiyor?

## 6. Rapor ve kayıt (20 dakika öneri)

Oturum kaydına senin yaptığın kısmı, AI desteğini, süreyi ve açık soruları yaz. Gereksinim sayfasını kısa tut; açıklama ve gerekçelerin ayrıntısını rapora ekle. Son olarak yapılan değişiklikleri inceleyip Git kaydına dönüştürmeyi öğren.

Kalan 30 dakika ilk tahminde ara/tekrar payıdır; süreler gerçekleşmiş çalışma değildir.

## Tamamlanma kontrolü

- [x] Kullanım senaryosu ve V0/V1/sonraki sürüm sınırları yazılı.
- [ ] Kısa kapsam ve sayısal hedefler son incelemeden geçti.
- [x] Alan çizimi var; 2 × 2 m alan ve 40 × 40 cm robot varsayım olarak kayıtlı.
- [x] Base/target/engel etiketleri ve gösterilen dar geçiş açıklıkları kayıtlı.
- [ ] Operatör yeri ve kesikli hatların merkez yolu olduğu notu net.
- [ ] İlk sayısal hedefler, birimler, gerekçeler ve ölçüm yöntemleri kayıtlı.
- [x] İlk doğrusal hız, faydalı yük ve çalışma süresi hedefleri gerekçeyle kaydedildi.
- [ ] Simülasyon ve fiziksel kabul için başarı eşikleri açık.
- [x] Arda'nın kendi ilk blok şeması var.
- [x] Arda haritalamadan hedefe harekete kadar kişisel senaryo açıklamasını sundu.
- [ ] Blok şemasında komut, geri besleme ve enerji yönleri/etiketleri incelemeden geçti.
- [ ] Arda komut, geri besleme ve enerji akışını kendi sözleriyle açıklayabiliyor.
- [x] Arda komut kaybında durma sorumluluğunun STM32'de olduğunu belirtti.
- [x] Arda motor sürücü ile enkoderin temel rol farkını kendi sözleriyle açıkladı.
- [ ] Arda son geçerli komut süresiyle timeout kontrolünü kendi sözleriyle açıklıyor.
- [x] Arda 250/450 ms alıştırmasında timeout durumunu doğru yorumladı.
- [ ] Katkı, süre ve kanıt yolları oturum kaydında.

Mevcut kanıt: evidence/AMR-01/ altında alan-cizimi-v01/v02.png ve blok-semasi-v01/v02/v03.png dosyaları; ayrıntılı yollar [inceleme kaydında](../sistem-mimarisi-inceleme.md). Timeout alıştırmasının 250/450 ms yorumu, uçtan uca kişisel senaryo ve ilk hız/yük/süre hedefleri alındı. Kalan sayısal eşikler, son akış açıklaması ve küçük yerleşim notları henüz bekleniyor. AMR-01 tamamlanmadı; çizimler bu görevin uygulama çıktıları, rapor ise bunların kaydıdır.

## Kalan işler: iki kapanış iş grubu

1. **Geçici sayısal gereksinimler:** ilk hız, yük ve süre; timeout/fiziksel duruş; V1 toleransları, başarı eşikleri ve engelde durma/bildirim davranışlarının tanımı. Gerekçe ve ölçüm yöntemiyle kayıt.
2. **Son inceleme ve kayıt:** kısa kapsam, kendi sözleriyle üç akış, laptop/robot sınırı ve kısa besleme/haberleşme/mekanik notları, operatör/merkez yolu notu, kanıt/katkı, gerçek aktif süre ve açık varsayımlar. Kabul karşılanırsa AMR-01 kapanır; donanım seçimi ve robot uygulaması sonraki görevlere aittir.
