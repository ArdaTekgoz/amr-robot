# AMR Robot

Arda TEKGÖZ'ün öğrenme odaklı otonom mobil robot geliştirme projesi.

Hedef: tek katlı bir iç mekânda diferansiyel sürüşlü robotla harita oluşturmak, kayıtlı haritada kullanıcının seçtiği erişilebilir konuma otonom gitmek ve başarıyı ölçmek.

İlk fiziksel teslimat **V0: gamepad ile kontrol edilen mobil platform** olacaktır. Gamepad başlangıç kontrol tercihidir; model/bağlantı yöntemi henüz seçilmedi. Haritalama ve otonom navigasyon V0 kabul koşulu değildir.

Ardından **V1: temel otonom AMR** geliştirilecektir. Haritalama sırasında robotu operatör gezdirir. Robot sensör verisinden haritayı oluşturur; kayıtlı haritada hedefe hareket otonomdur. A/B veya base/target noktaları tekrarlı kabul deneyinde kullanılır. Modüler üst yapı, QR/görüntü işleme, periyodik görev ve kendi kendine keşif sonraki sürümlerdir. TEKNOFEST için altyapı oluşturma uzun vadeli amaçtır; yarışma şartnamesi henüz incelenmedi.

## Mevcut durum

- Aktif görev: **AMR-01 - Görev tanımı ve sistem sınırları**; durum: devam ediyor.
- ROS 2 daha önce Docker üzerinden kurulmuş; sürüm ve çalışır durum AMR-02'de doğrulanacak.
- Harici laptop ve kablosuz robot bağlantısı başlangıç adayı; robot tarafı haberleşme birimi/protokol henüz seçilmedi.
- STM32 Nucleo alınması planlanıyor; model seçilmedi. Motor, enkoder, sürücü ve sensör mevcut değil.
- Test mekânı ve sayısal performans hedefleri henüz belirlenmedi.
- Robot kodu ve deney sonucu henüz yok. Depo başlangıcı, uygulama başarısı değildir.

## Çalışma biçimi

Arda kritik tasarım ve uygulamayı yapar; AI danışman olarak açıklama, inceleme ve hata ayıklama sağlar. Her görev: beklenen davranış → Arda'nın denemesi → doğrulama → kanıt → rapor.

## Belgeler

- [Bugünkü görev](docs/gorevler/AMR-01.md)
- [Kullanıcı vizyonu ve teslimat kapsamı](docs/vizyon-ve-kapsam.md)
- [V0 manuel platform gereksinimleri](docs/gereksinimler-v0.md)
- [V1 otonom AMR gereksinimleri](docs/gereksinimler-v1.md)
- [Yol haritası ve kabul kapıları](docs/yol-haritasi.md)
- [Gelişen proje raporu](docs/rapor.md)
- [İlk oturum kaydı](docs/oturumlar/2026-10-12-AMR-01.md)
- [13 Ekim oturum kaydı](docs/oturumlar/2026-10-13-AMR-01.md)
- [Kanıt düzeni](evidence/README.md)
- [Başlangıç raporu](amr-rapor.pdf)

STM32 motor kontrolü ve telemetriyi; ROS 2 bilgisayarı odometri, TF, haritalama, konumlanma, navigasyon ve görev yönetimini üstlenecek. Ayrıntılı arayüz ve parça seçimi ilgili görevlerde kesinleştirilecek.

V0 ara teslimatı AMR-21 düzeyinde telefon/kumanda uçtan uca kontrolüyle kabul edilir; simülasyon V1 AMR-11, fiziksel V1 AMR-24 ile kapanır. Başarısız denemeler de raporlanır.
