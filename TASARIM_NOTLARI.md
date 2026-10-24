# Tasarım Notları ve Yapılacaklar

Bu dosya, üst çubuk ve uygulama başlatıcısı fikrinin uygulanabilir parçalara ayrılmış kontrol listesidir. Maddeler, gerçekten test edilip tamamlanana kadar tamamlanmış sayılmaz.

## İlk kurulum

- [ ] ThinkPad T480 donanımını, ekran çözünürlüğünü ve pil raporlamasını kontrol et
- [ ] Arch Linux kurulumunu tamamla
- [ ] Sway oturumunu ve temel giriş aygıtlarını doğrula
- [ ] Ses, Wi-Fi, Bluetooth ve parlaklık kontrolünü test et
- [ ] Pil bilgilerine erişilebildiğini kontrol et

## Uygulama başlatıcısı

- [ ] Super tuşuna basıldığında uygulama başlatıcısını aç
- [ ] GNOME tarzı tam ekran uygulama ızgarası yerine küçük, koyu temalı ve ortalanmış bir pencere kullan
- [ ] Uygulama adını yazarak arama ve sonuçları filtreleme işlevini doğrula
- [ ] Sonuçlar arasında klavyeyle gezinmeyi ve uygulama başlatmayı test et
- [ ] Esc tuşuyla başlatıcıyı kapat
- [ ] Başlatıcının kaynak tüketimini ve açılma hızını ölç
- [ ] Başlatıcı aracı olarak `wofi` veya `bemenu` seçeneklerini bağımlılık ve kullanım açısından karşılaştır; seçim yapmadan ikisini birden kurma

## Üst çubuk

- [ ] Waybar'ı sabit, yaklaşık 32 piksel yüksekliğinde yapılandır
- [ ] Koyu temayı ve aralıkları ayarla
- [ ] Sol: CPU ve bellek göstergeleri
- [ ] Sol: anlık indirme / gönderme hızları
- [ ] Orta: Spotify parça adı ve medya kontrolleri
- [ ] Orta: saati ayrı blokta göster; medya süresiyle karışmadığını kontrol et
- [ ] Sağ: ağ, Bluetooth, parlaklık, pil, uptime ve çalışma alanları
- [ ] Uzun parça adlarında taşma ve hizalama sorunlarını test et

## Ayrıntı panelleri

- [ ] Ağ oturumu toplam indirme verisi
- [ ] Ağ oturumu toplam gönderme verisi
- [ ] Anlık hızları toplam sayaçlardan ayrı göster
- [ ] Pil kalan süre tahmini (varsa)
- [ ] Tam dolum kapasitesi ve tasarım kapasitesi (varsa)
- [ ] Döngü sayısı (varsa)
- [ ] Eksik veriler için anlaşılır geri dönüş metni

## Son kontroller

- [ ] Bellek ve işlemci tüketimini ölç
- [ ] Uyku/uyanma sonrasında göstergeleri kontrol et
- [ ] Ağ bağlantısı kesilip geldiğinde sayaç davranışını kontrol et
- [ ] Parça değiştiğinde saatin yeri sabit kalıyor mu kontrol et
- [ ] Türkçe karakterleri ve metin taşmalarını kontrol et
- [ ] Kullanılan paketleri ve kurulum adımlarını belgeye ekle
