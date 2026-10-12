# AMR Robot - Gelişen Proje Raporu

Yazar: Arda TEKGÖZ. Başlangıç: 12 Ekim 2026. Revizyon: 0.2. Belge türü: bitirme projesi düzeninde çalışma taslağı; kurumun biçim şartları henüz verilmedi.

## Özet

Bu proje, tek katlı bir iç mekânda diferansiyel sürüşlü mobil robotla harita oluşturmayı ve kayıtlı haritada kullanıcının seçtiği erişilebilir konuma otonom hareket etmeyi amaçlar. STM32 tabanlı tekerlek kontrolü ile ROS 2 tabanlı navigasyon katmanı ayrı geliştirilecek, sonra fiziksel sistemde birleştirilecektir. Simülasyon ve fiziksel robot kabulü ayrı deneylerle değerlendirilecektir. Henüz uygulama veya performans sonucu yoktur.

İlk fiziksel ara teslimat V0, telefon veya kumandayla kontrol edilebilen mobil platformdur. Ardından temel otonom işlevler V1'de geliştirilecektir. Proje kişisel yetkinlik kazanımı ve ileride TEKNOFEST Sanayide Robotik Teknolojiler yarışmasına teknik altyapı oluşturma amacı taşır. Yarışma şartnamesi henüz değerlendirilmemiştir.

## 1. Problem, amaç ve kapsam

İlk haritalamada operatör robotu gezdirecek; sensör verisinden harita oluşturulacaktır. Hedefe otonom hareket kayıtlı haritada gerçekleşecektir. Ortamı kendi kendine keşfetme sonraki sürüme bırakılmıştır. A/B istasyonları, seçilebilir hedef yeteneği için tekrarlı test noktalarıdır.

Arda'nın kendi problem tanımı altı maddelik kullanım senaryosuyla sunuldu ve [vizyon/kapsam kaydında](vizyon-ve-kapsam.md) anlamı korunarak düzenlendi. Uzun vadede farklı düz zeminli mekânlarda yeniden haritalama, harita arayüzünde base/target seçimi, hedefte bekleme ve dönüş, kapalı yolda alternatif rota, QR ile görev zinciri ve modüler görüntü işleme işlevleri hedeflenir. İlk fiziksel teslimatın asgari kabulü manuel mobil platformdur.

Kapsam ve ölçülebilir hedefler: [V0 gereksinimleri](gereksinimler-v0.md) ve [V1 gereksinimleri](gereksinimler-v1.md). Gerçek test mekânı henüz seçilmedi; varsayımsal simülasyon boyutları fiziksel ölçüm diye sunulmayacaktır. “Her ortama uyum” bütün ortamların doğrulandığı anlamına gelmez; zemin/geometri/sensör koşulları kabul deneyinde sınırlandırılacaktır.

## 2. Başlangıç durumu ve yöntem

Arda'nın beyanı: ROS 2 Docker üzerinden daha önce kurulmuştur; Python ve C/C++ kodlarını analiz etme, takip etme ve gerektiğinde düzenleme deneyimi vardır. ROS 2'yi öğrenmek istemektedir. STM32 Nucleo alımı planlanmaktadır; kart modeli ve diğer parçalar seçilmemiştir. Motor, enkoder, sürücü ve sensör mevcut değildir. Kurulumun sürümü ve çalışırlığı henüz doğrulanmamıştır.

Yöntem: ihtiyacı tanımlama, tasarım/hesap, Arda'nın uygulaması, beklenen-gerçek karşılaştırması, kanıt ve raporlama. Her deneyin ortamı SIM veya FİZ olarak etiketlenecek; başarısız denemeler de saklanacaktır. AI danışmanlık ve belge düzenleme desteği sağlayacaktır.

## 3. İlgili çalışmalar ve teknik kaynaklar

Başlangıç kaynağı: ../amr-rapor.pdf, 12 Ekim 2026, 19 sayfa. Yol haritası ve görevler incelendi. Teknik kaynaklar ilgili uygulama görevinde okunup sürüm ve erişim tarihiyle kaydedilecek. Başlangıç PDF'sinde listelenen web kaynakları bu oturumda ayrıca doğrulanmadı.

Kaynak kayıt biçimi: başlık, üretici/yazar, sürüm, URL, erişim tarihi, projede desteklediği karar. Literatür değerlendirmesi henüz yapılmadı.

## 4. Gereksinimler ve sistem mimarisi

Üst düzey rol ayrımı: STM32 PWM, enkoder okuma, sabit periyotlu hız kontrolü ve komut zaman aşımını; ROS 2 bilgisayarı odometri, TF, SLAM, konumlanma, navigasyon ve görev yönetimini üstlenecek. Motor sürücü, kontrol sinyalini motor gücüne aktaracak. Ayrıntılı arayüz henüz tasarlanmadı.

Arda'nın blok şeması ve üç akış açıklaması: **bekleniyor**.

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

Sayısal hedeflerin gerekçeleri: **Arda yazacak**.

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

Arda: kullanım hedefini, başlangıç deneyimini/donanım durumunu ve ilk haritalama yöntemini açıkladı; altı maddelik senaryosunda kişisel gelişim/yarışma altyapısı amacını, modüler robot vizyonunu ve manuel ilk prototip beklentisini belirledi. Teknik çizim, sayısal gereksinim ve uygulama henüz sunulmadı.

AI: mevcut raporu inceledi; depo, yol haritası, çalışma sayfaları ve rapor iskeletini hazırladı. Bu hazırlık Arda'nın teknik uygulama kanıtı değildir.

Her görevde Arda'nın kendi açıklaması ve öğrendiği konu [oturum kaydında](oturumlar/2026-10-12-AMR-01.md) tutulacak.

## Ekler

- [Yol haritası](yol-haritasi.md)
- [AMR-01 çalışma yönergesi](gorevler/AMR-01.md)
- [Kanıt kayıt düzeni](../evidence/README.md)
- İleride: BOM, bağlantı şeması, protokol, hesaplar, deney CSV'leri, kurulum ve demo.
