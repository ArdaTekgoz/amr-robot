# AMR Robot

Arda TEKGÖZ'ün öğrenme odaklı otonom mobil robot geliştirme projesi.

Hedef: tek katlı bir iç mekânda diferansiyel sürüşlü robotla harita oluşturmak, kayıtlı haritada kullanıcının seçtiği erişilebilir konuma otonom gitmek ve başarıyı ölçmek.

İlk sürümde haritalama sırasında robotu operatör gezdirir. Robot sensör verisinden haritayı oluşturur; kayıtlı haritada hedefe hareket otonomdur. Kendi kendine ortam keşfi sonraki sürümdür. A/B istasyonları tekrarlı kabul deneyinin hedefleridir.

## Mevcut durum

- Aktif görev: **AMR-01 - Görev tanımı ve sistem sınırları**; durum: devam ediyor.
- ROS 2 daha önce Docker üzerinden kurulmuş; sürüm ve çalışır durum AMR-02'de doğrulanacak.
- STM32 Nucleo alınması planlanıyor; model seçilmedi. Motor, enkoder, sürücü ve sensör mevcut değil.
- Test mekânı ve sayısal performans hedefleri henüz belirlenmedi.
- Robot kodu ve deney sonucu henüz yok. Depo başlangıcı, uygulama başarısı değildir.

## Çalışma biçimi

Arda kritik tasarım ve uygulamayı yapar; AI danışman olarak açıklama, inceleme ve hata ayıklama sağlar. Her görev: beklenen davranış → Arda'nın denemesi → doğrulama → kanıt → rapor.

## Belgeler

- [Bugünkü görev](docs/gorevler/AMR-01.md)
- [Gereksinim çalışma sayfası](docs/gereksinimler-v1.md)
- [Yol haritası ve kabul kapıları](docs/yol-haritasi.md)
- [Gelişen proje raporu](docs/rapor.md)
- [İlk oturum kaydı](docs/oturumlar/2026-10-12-AMR-01.md)
- [Kanıt düzeni](evidence/README.md)
- [Başlangıç raporu](amr-rapor.pdf)

STM32 motor kontrolü ve telemetriyi; ROS 2 bilgisayarı odometri, TF, haritalama, konumlanma, navigasyon ve görev yönetimini üstlenecek. Ayrıntılı arayüz ve parça seçimi ilgili görevlerde kesinleştirilecek.

Simülasyon v1 AMR-11, fiziksel v1 AMR-24 ile kapanır. Başarısız denemeler de raporlanır.
