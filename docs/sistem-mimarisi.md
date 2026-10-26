# Sistem mimarisi ve açılış planı

Bu belge, ThinkPad T480 üzerinde kurulması planlanan Arch Linux sisteminin açılış zinciri, init sistemi ve NEPHELO açılış görseli için alınan tasarım kararlarını toplar. Bunlar henüz uygulanmış veya test edilmiş bir sistemin açıklaması değildir.

## Temel tercihler

- **Dağıtım:** Arch Linux
- **Dosya sistemi:** ext4
- **Init / servis yönetimi:** s6 ekosistemi değerlendiriliyor; hedef olarak `s6-linux-init`, `s6` ve `s6-rc` düşünülüyor.
- **İlke:** Küçük, modüler, anlaşılır ve gereksiz karmaşıklıktan uzak bir sistem.
- **Durum:** Planlama aşaması. Donanımın gerçek yapılandırması ve açılış zinciri kurulum sırasında doğrulanacak.

## Initramfs kararı: açık bırakıldı

Initramfs kullanmamak bir zorunluluk değil. `mkinitcpio` yapılandırmasındaki sorunları düzeltmek kolaysa, standart initramfs ile devam etmek daha pratik ve bakımı daha kolay bir seçim olabilir.

İki seçenek de değerlendirilebilir:

1. **Varsayılan / düşük riskli yol:** `mkinitcpio` ve initramfs ile devam et; sorun çıkaran hook veya yapılandırmayı belirleyip düzelt.
2. **İsteğe bağlı deney:** Kernel ve donanım yapılandırması uygunsa initramfs olmadan doğrudan kök dosya sisteminden açılmayı dene.

Initramfs’sız açılış şimdilik yalnızca deneysel bir seçenek. Uygulanacağı garanti edilmiyor; zaman veya emek maliyeti ağır gelirse initramfs ile kalınabilir.

## Initramfs’sız açılış için teknik koşullar

Initramfs olmadan kernel, gerçek kök dosya sistemini kendisi bulup bağlayabilmelidir. Bunun için yalnızca ext4 desteğinin bulunması yetmez; kök bölüme erişmek için gereken sürücüler de kernel içine yerleşik derlenmelidir, modül olarak bırakılmamalıdır.

Kurulumdan önce en azından şu başlıklar doğrulanmalı:

- UEFI ve bootloader yapılandırması
- Kök bölümün gerçek UUID’si ve doğru `root=UUID=…` parametresi
- Bölüm tablosu ve depolama denetleyicisi desteği
- ext4 desteğinin kernel içine yerleşik olması (`CONFIG_EXT4_FS=y`)
- Gerekli PCI / NVMe / SATA / AHCI ve diğer donanım sürücülerinin gerçek donanıma göre yerleşik olması
- `/dev`, `/proc` ve `/sys` dosya sistemlerinin erken açılışta doğru kurulması

Bunlar kontrol listesi başlangıcıdır; T480’ın kesin donanım yapılandırması görülmeden eksiksiz kernel seçenekleri listesi varsayılmamalıdır. EFI stub seçeneği de tek başına initramfs’sız açılışın garantisi değildir; kullanılacak bootloader’ın kernel’i nasıl yüklediği ayrıca belirlenmelidir.

## Önerilen uygulama sırası

1. T480’ın tam donanım yapılandırmasını ve mevcut açılış biçimini kaydet.
2. Mevcut sistemin yedeğini ve çalışan bir kurtarma USB’sini hazırla.
3. Önce mevcut initramfs / `mkinitcpio` sorunlarını teşhis et; basit bir düzeltme yeterliyse initramfs ile devam et.
4. Initramfs’sız açılış hâlâ isteniyorsa bunu ayrı, geri alınabilir bir deneme olarak hazırla. Mevcut çalışan kernel ve boot girdisini silme.
5. Init sistemi geçişini ayrı bir adımda ele al. Kernel açılışını ve initramfs seçimini aynı anda değiştirme.
6. s6 kurulumu ve servis zinciri doğrulandıktan sonra NEPHELO açılış görselini dene.

Her aşamada bir değişkeni değiştirmek, açılmayan sistemde sorunun kaynağını bulmayı kolaylaştırır.

## s6 ve servis yönetimi

Değerlendirilen bileşenler:

- `s6-linux-init`: PID 1 / sistem başlatma katmanı
- `s6`: servisleri izleme ve süreç gözetimi
- `s6-rc`: servis bağımlılıkları ve servislerin başlatılıp durdurulması

Bunlar henüz kurulmuş bir yapı değil, planlanan adaylardır. Gerçek yapılandırma; aygıt düğümlerinin hazırlanması, sanal dosya sistemlerinin bağlanması, gerekli temel servisler ve oturum başlatma sırası doğrulanarak oluşturulmalıdır. PID 1 geçişinden önce kurtarma yolu ve eski açılış seçeneği korunmalıdır.

## NEPHELO açılış görseli

### Görsel fikir

- Siyah arka plan
- Beyaz, geometrik bir bulut silüetinden oluşan logo
- Kısa terminal metni
- Yaklaşık 2–3 saniyelik, sade bir geçiş
- Gösterişten çok hızlı ve tutarlı açılış

### Uygulama notu

Görselin ne zaman gösterileceği seçilen açılış zincirine bağlıdır. Initramfs kullanılmazsa initramfs aşamasında çalışan bir animasyon yolu da olmayacaktır. Bu nedenle ilk prototip, kök dosya sistemi bağlandıktan ve temel kullanıcı alanı servisleri başladıktan sonra gösterilen bir konsol / framebuffer animasyonu olabilir. Daha erken aşama için bootloader’ın statik görsel desteği ayrı değerlendirilebilir.

Animasyon, açılışın güvenilirliğinden ve hata mesajlarının görülebilirliğinden daha önemli değildir. Sorun giderme sırasında animasyon kapatılabilmelidir.

## Henüz kesinleşmeyenler

- Initramfs ile devam mı edilecek, initramfs’sız açılış denenecek mi?
- T480’ın kesin işlemci, depolama denetleyicisi ve disk yapılandırması
- Kullanılacak kernel ve bootloader ayarları
- s6 servis tanımları ve oturum başlatma yöntemi
- NEPHELO animasyonunun gerçek uygulama yöntemi

Bu kararlar donanım ve çalışan kurulum üzerinden doğrulandıktan sonra kesinleştirilecek.
