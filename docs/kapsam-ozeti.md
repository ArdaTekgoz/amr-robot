# AMR - İlk kapsam ve kabul özeti

13 Ekim 2026 | AMR-01 son inceleme taslağı | Arda TEKGÖZ

## Amaç ve teslimatlar

Kişisel mühendislik yetkinlikleri ve ileride yarışma altyapısı için, düz zeminli tek katlı iç mekânda diferansiyel sürüşlü modüler mobil platform geliştirmek.

- **V0:** Gamepad ile manuel sürüş, ölçülen motor kontrolü, odometri kalibrasyonu, komut kaybında durma ve doğrulanmış güç düzeni.
- **V1:** Operatör gezdirirken LiDAR adayıyla harita oluşturma; kayıtlı haritada hedef/base seçimi, otonom hedefe gidiş, bekleme/dönüş, algılanan engelde durma ve uygun alternatif rota davranışı; ses/LED durum bildirimi.
- **Sonraki kapsam:** QR görev zinciri, görüntüyle hedef algılama, periyodik görev, otonom keşif ve üretilmiş üst modül.

## Sınırlar ve sorumluluklar

İlk varsayımsal alan 2 × 2 m; gövde 40 × 40 cm; iki rota fikri. Gerçek alan seçilmedi. Dönüş açıklığı, hedeflerin duvara uzaklığı ve sensör kapsaması sonraki model/deneylerde doğrulanacak.

Harici laptop kendi beslemesiyle ROS 2/Nav2 haritalama, konumlanma, rota ve güncel hız komutlarını yürütür. Robotta kablosuz arayüz aday; STM32 sürücüleri kontrol eder, enkoder/mesafe geri beslemesini işler, komut timeout'unu uygular. Motor enerjisi sürücüden motora gider. Model, protokol ve gerilim dağıtımı henüz seçilmedi.

## Geçici hedefler ve doğrulama

| Hedef | Değer | Doğrulama |
| --- | --- | --- |
| Seyir / azami hız | 0,25–0,35 m/s / boş yük ve geniş alanda 0,45 m/s | Referans/ölçüm logu; koşullar ayrı |
| Faydalı yük | 5 kg; bütçe ile gerekçeli 3 kg revizyonu mümkün | Geçerli revizyondaki yükle rota |
| Çalışma | ≥30 dk; 5 kg, nominal çevrim, ilgili sensörler açık | Tanımlı çevrim ve robot batarya kaydı |
| Hedef hatası | Toplam konum ≤5 cm; yön ≤5° | SIM dünya referansı / FİZ bağımsız ölçüm |
| Normal görev başarısı | SIM ≥8/10; FİZ ≥6/10 | Sabit on deney; bütün sonuçlar kayıtlı |
| Komut kaybı | Danışman önerisi: 20 Hz komut, ≥250 ms güncel komut yoksa ilk kontrol çevriminde sıfır referans | Kesinti, geçersiz/eski mesaj, gecikme ve gerçek duruş ayrı ölçülür |

5 cm bütçeyle doğrulanmazsa 6–7 cm gerekçeli revizyon değerlendirilebilir. Timeout, donanım ve bağlantı ölçümüyle değişebilir; sıfır referans tam mekanik duruş demek değildir. İptal/bağlantı kaybı/engel duruşu ve diğer V1 gereksinimleri, görev başarı oranından ayrı kabul edilir.

## Açık kararlar ve kanıt

AMR-12: motor/enkoder/sürücü, 12 V motor adayı, pil kapasitesi, uygun beslemeler, fiziksel duruş sınırı ve kablolu şarj. AMR-04/06/16: açısal sınırlar ve kontrol periyotları. AMR-10/11/23: sabit rota/çevrim, görev süresi, engel/yeniden başlama ve bildirim ayrıntıları. Testten önce ilgili koşullar dondurulur.

Kanıtlar: [alan](test-alani.md), [kişisel blok şemaları ve inceleme](sistem-mimarisi-inceleme.md), [13 Ekim oturumu](oturumlar/2026-10-13-AMR-01.md). Toplam aktif süre: **yaklaşık 3 saat, kullanıcı tahmini**; günlere ayrılmış ölçüm yok. Robot deneyi yapılmadı. AMR-01 son kişisel açıklama ve kayıt incelemesi bekliyor.
