# Kullanıcı vizyonu ve teslimat kapsamı

12 Ekim 2026. Kaynak: Arda'nın altı maddelik kullanım senaryosu ve önceki haritalama seçimi. Aşağıdaki metin anlamı korunarak AI tarafından düzenlenmiştir; uygulama sonucu değildir.

## Arda'nın kullanım amacı

1. Proje kişisel gelişim ve ileride TEKNOFEST Sanayide Robotik Teknolojiler yarışması için teknik altyapı oluşturmayı amaçlar. Uzun vadede modüler üst yapı taşıyabilen, otonom hareket eden ve görüntü işlemeyle hedef algılayan bir robot hedeflenir. Yarışma şartnamesi henüz incelenmedi; yarışmaya uygunluk iddiası yoktur.
2. Düz zeminli farklı iç mekânlarda operatör robotu kumandayla gezdirerek harita oluşturur. Ardından haritadaki hedeflere otonom hareket ve engel durumuna uygun davranış geliştirilir. “Her ortam” bir vizyondur; ilk kabul tanımlı bir test ortamında yapılır.
3. Harita arayüzünden base ve target seçilir. İleride görev belirli aralıklarla tekrarlanabilir veya istasyondaki QR kod sonraki hedefi belirleyebilir.
4. Hedefte tanımlı süre bekleme ve base'e dönüş; ileride QR ile başka hedefe geçiş amaçlanır.
5. Geçiş kapalıysa robot alternatif rota bulabilmelidir. Alternatif rota da yoksa davranış ayrıca tanımlanacaktır.
6. İlk fiziksel prototip için asgari beklenti telefon veya kumandayla kontrol edilebilen mobil platformdur. İleri otonom işlevler bu ilk teslimatın koşulu değildir.

## Aşamalı teslimatlar

| Teslimat | Kapsam | Kabul dışında kalanlar |
| --- | --- | --- |
| V0 - Manuel mobil platform | Düz zeminde ileri/geri/dönüş/durma; seçilecek tek telefon veya kumanda arayüzü; bağlantı kaybında durma; kontrol ve güç doğrulaması | SLAM, otonom hedefe gitme, otomatik engelden kaçınma, QR ve görüntü işleme |
| V1 - Temel otonom AMR | Operatör eşliğinde harita, kayıtlı haritada hedef seçme, konumlanma, otonom navigasyon, algılanan engelde uygun alternatif rotayı deneme, erişilemez hedefte durum bildirimi; temel base-target-bekle-base görev dizisi | Periyodik görev zamanlama, QR görev zinciri, görüntüyle hedef tanıma, otonom keşif |
| Sonraki sürümler | Modüler uygulama üst yapısı, QR/görüntü işleme, periyodik görev, otonom keşif ve yarışmaya özgü işlevler | Ayrıntılı kapsam, ek donanım ve süre henüz belirlenmedi |

V0, kaynak rapordaki fiziksel V1'in öncesine eklenen bir ara teslimattır. Kaynak görev numaraları korunur. İlk fiziksel ürün asgari V0; ana yol haritasının otonom hedefi V1'dir. SIM V1 ve FİZ V1 ayrı kabul edilir.

Tek kontrol arayüzü V0 için yeterlidir; telefon ve kumandanın ikisini birden geliştirmek henüz bir gereksinim değildir. Arayüz ve bağlantı yöntemi henüz seçilmedi. Telefon/kumanda kullanımının kullanıcı komutundan STM32'ye kadar uçtan uca kabulü V0 kapanışına dahildir.

Modülerlik başlangıç mekanik tasarımında göz önüne alınacak; bağlantı ölçüsü, yük, ağırlık merkezi ve güç/veri arayüzleri AMR-12/20'de gerekçelendirilecek. Üst modül bu aşamada üretilmeyecek.

## Engel davranışının sınırı

V0'da çevreyi operatör gözler ve sürüşe karar verir. Otomatik kaçınma kabulü yoktur.

V1'de hedef, algılanan engel karşısında uygun geçilebilir rota varsa yeniden planlamak; rota yoksa belirlenen yeniden deneme/süre sınırı içinde görevi başarısız veya beklemede bildirmektir. Süre, hız, durma mesafesi, sensör kapsaması ve sınırlar henüz seçilmedi. Robotun bütün engelleri her ortamda algılayabildiği varsayılmaz.
