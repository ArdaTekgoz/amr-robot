# AMR-01 - Görev tanımı ve sistem sınırları

Tarih: 12 Ekim 2026. Tahmin: 4 saat. Gerçek süre: henüz kaydedilmedi. Durum: devam ediyor. Donanım gerekmez.

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

**Şu anki uygulama adımı budur.** Alan çizimini tekrar tekrar ayrıntılandırmak yerine sistem blok şemasına geçilecek. Telefon/kumanda arayüzünü de bloklara ekle. Henüz model, pin, gerilim veya haberleşme teknolojisi seçmek gerekmiyor.

STM32, ROS 2 bilgisayarı, motor sürücü, motorlar, enkoderler, mesafe sensörü ve güç kaynağı için bloklar çiz. Her okun üzerine “ne taşınıyor?” yaz. Komut, geri besleme ve enerji için ayrı ok biçimi/renk seç.

Kendine sor: Hedef koordinatı ile motor sürme komutu aynı şey mi? Enkoder bana hangi ölçümü verir? Motor enerjisini hangi blok sağlar? Bilgisayardan mesaj gelmezse hangi blok karar vermeli?

**Neden:** Veriyi, kontrol kararını ve gücü ayırmak entegrasyon hatalarını bulmayı kolaylaştırır. Hazır şemayı kopyalamak yerine kendi şemanı açıklaman bekleniyor.

## 4. Gereksinimleri ölçülebilir yaz (50 dakika öneri)

[Çalışma sayfasını](../gereksinimler-v1.md) doldur. Hız, yük, çalışma süresi, konum/açı toleransı, başarı eşiği ve duruş davranışı için geçici hedef + gerekçe + ölçüm yöntemi yaz. Parça alımına bağlanan değerler AMR-12'de tekrar değerlendirilecek.

Önce [V0 çalışma sayfasındaki](../gereksinimler-v0.md) manuel kontrol hedeflerini seç; V1 konumlanma ve navigasyon hedeflerini ayrı tut. Telefon veya kumandadan hangisinin ilk kontrol arayüzü olacağı henüz açık bir karardır.

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
- [ ] Simülasyon ve fiziksel kabul için başarı eşikleri açık.
- [ ] Arda'nın kendi blok şeması var.
- [ ] Arda komut, geri besleme ve enerji akışını kendi sözleriyle açıklayabiliyor.
- [ ] Katkı, süre ve kanıt yolları oturum kaydında.

Mevcut kanıt: evidence/AMR-01/alan-cizimi-v01.png ve alan-cizimi-v02.png. Arda'nın blok şeması ve ilk sayısal performans hedefleri henüz bekleniyor. AMR-01 tamamlanmadı; çizim bu görevin bir uygulama çıktısı, rapor ise bunun kaydıdır.
