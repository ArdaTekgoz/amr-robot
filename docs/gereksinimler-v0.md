# V0 - Manuel mobil platform gereksinimleri

Revizyon: 0.1 taslak | 12 Ekim 2026 | Durum: kapsam belirlendi; sayısal hedef ve kontrol arayüzü bekleniyor.

İlk fiziksel prototip: düz zeminde operatörün telefon veya kumanda üzerinden hareket ettirebildiği diferansiyel sürüşlü platform. Bu teslimat, otonom AMR geliştirmesinin hareket tabanıdır.

| ID | Gereksinim | Doğrulama |
| --- | --- | --- |
| V0-01 | Seçilecek tek arayüzden ileri, geri, sağ/sol dönüş ve durma komutları | Tanımlı test alanında her komut için beklenen/gerçek hareket kaydı |
| V0-02 | Komut bırakılınca belirlenen davranışla durma; başlangıç/reset sonrasında istemsiz hareket olmaması | Başlangıç, reset ve komut bırakma deneyi; davranış/süre seçilecek |
| V0-03 | Geçerli komut kaybında STM32'nin belirlenen timeout ile sıfır referansa geçmesi | Bağlantı kesme: son geçerli mesaj, sıfır referans ve gerçek duruş sürelerini ayrı ölç |
| V0-04 | Hız sınırı ... m/s; açısal hız ... rad/s | Referans ve ölçülen tekerlek/gövde hızlarını karşılaştır |
| V0-05 | ... dakika tanımlı kullanım; faydalı yük ... kg | Görev çevrimi, yük ve süre kayıtlı fiziksel deney |
| V0-06 | Motor enerjisini fiziksel olarak kesebilme; kablo/güç düzeninin doğrulanması | AMR-20 güç kontrolü ve enerjiyi kesme deneyi |
| V0-07 | Ölçülen tekerlek kontrolü ve odometri kalibrasyonu | AMR-19 ve AMR-21 sonuçları; otonom navigasyon gerektirmez |

Telefon/kumanda türü, haberleşme yöntemi, hız, yük, süre, timeout, fiziksel duruş eşiği ve tekrar sayısı henüz seçilmedi. V0-07 öğrenme hedefleriyle mevcut görev bağımlılıklarını korur. Gereksinimler ölçülmeden V0 tamamlandı denmez.

V0 dışı: harita, otonom rota, otomatik engelden kaçınma, QR, görüntü işleme, görev zamanlama ve üretilmiş üst modül. Modülerliğe yönelik mekanik paylar AMR-12/20'de planlanacak.
