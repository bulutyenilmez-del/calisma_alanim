# Çalışma Alanım

Bu depo, ileride ThinkPad T480 üzerinde kuracağım Arch Linux sistemim ve kendime göre tasarlayacağım üst çubuk arayüzü için Türkçe çalışma notlarını içerir.

## Projenin amacı

Sade, koyu temalı, sabit duran ve düşük kaynak tüketen bir üst çubuk hazırlamak. Sistem göstergeleri ilk bakışta anlaşılır olacak; ayrıntılar gerektiğinde tıklamayla açılacak.

Bu depo şimdilik bir **tasarım ve uygulama planıdır**. Donanım ve sistem hazır olduğunda adım adım uygulamaya geçilecek; henüz çalışan bir uygulama olduğu varsayılmamalıdır.

## Temel ortam

- **Bilgisayar:** ThinkPad T480
- **Dağıtım:** Arch Linux
- **Pencere yöneticisi / birleştirici:** Sway (Wayland) — başlangıç tercihi; kurulum sırasında doğrulanacak
- **Üst çubuk:** Waybar
- **Müzik kontrolü:** Spotify, MPRIS ve `playerctl`
- **Yaklaşım:** Hafif, modüler, okunabilir; gereksiz bağımlılıklardan kaçınan yapı
- **Dil:** Bu depodaki açıklamalar, planlar ve kullanıcıya dönük metinler Türkçe olacak. Kod ve yapılandırma sözdizimi doğal olarak kendi dil kurallarını izleyebilir.

## Uygulama başlatıcısı

Super tuşuna basıldığında uygulama başlatıcısı açılacak. GNOME'daki tam ekran uygulama ızgarası kullanılmayacak; bunun yerine sade, koyu temalı ve ekranın ortasında açılan küçük bir pencere tercih edilecek.

- Uygulamalar adları yazılarak aranabilecek ve sonuçlar yazdıkça filtrelenecek.
- Sonuçlar arasında klavyeyle gezinilebilecek ve uygulama başlatılabilecek.
- Esc tuşu pencereyi kapatacak.
- Başlatıcı hızlı açılmalı, az kaynak tüketmeli ve gereksiz görsel efektlerden kaçınmalı.
- Aday araçlar: `wofi` ve `bemenu`. Donanım ve bağımlılıklar göz önünde bulundurularak biri seçilecek; ikisini birden kurmak gerekmiyor.

Super tuşunun doğrudan başlatıcıyı açması Sway yapılandırmasında uygulanıp test edilecek. Kesin tuş eşlemeleri, kurulum sırasında diğer kısayollarla çakışma olup olmadığı kontrol edilerek belirlenecek.

## Üst çubuğun yerleşimi

Üst çubuk sabit olacak, otomatik gizlenmeyecek ve yaklaşık 32 piksel yüksekliğinde başlayacak. Görsel tasarım uygulama sırasında ekran çözünürlüğü ve okunabilirliğe göre ayarlanacak.

### Sol bölüm — sistem yükü ve ağ trafiği

- Anlık ağ indirme ve gönderme hızı
- İşlemci kullanımı
- Bellek kullanımı

### Orta bölüm — müzik ve saat

- Spotify parça adı ve mümkün olduğunda sanatçı adı
- Önceki parça, oynat/duraklat ve sonraki parça kontrolleri
- Saat, medya kontrollerinden **ayrı bir görsel blokta** bulunacak

Saatin şarkının geçen süresi veya toplam süresi sanılmaması önemli:

- Saat 24 saat biçiminde, örneğin `08:16`, saniyesiz gösterilecek.
- Medya kontrollerinden ince bir ayırıcı ve yeterli boşlukla ayrılacak.
- Saatin konumu parça adı değiştikçe kaymayacak.
- Parça adı uzunsa saatin alanını daraltmak yerine parça adı kısaltılacak.

### Sağ bölüm — bağlantı, güç ve çalışma alanları

- Wi-Fi / ağ bağlantısı
- Bluetooth
- Ekran parlaklığı
- Pil durumu
- Çalışma süresi (uptime)
- Sway çalışma alanları

## Tıklamayla açılacak ayrıntılar

Üst çubukta yalnızca kısa ve okunaklı göstergeler yer alacak. Ayrıntılar ilgili göstergeye tıklanınca açılacak.

### Ağ ayrıntıları

- Geçerli oturumda alınan toplam veri
- Geçerli oturumda gönderilen toplam veri
- Anlık indirme ve gönderme hızları ayrı değerler olarak gösterilecek

Toplam veri ile anlık hız birbirine karıştırılmayacak. Sayaçların hangi arayüzü ve hangi zaman aralığını kapsadığı açıkça belirtilecek.

### Pil ayrıntıları

Donanım ve sürücülerin sunduğu ölçüde:

- Tahmini kalan süre
- Mevcut tam dolum kapasitesi
- Tasarım kapasitesi
- Pil döngü sayısı

Her cihaz bu değerlerin tümünü sağlamayabilir; bulunmayan veriler uydurulmayacak ve arayüzde uygun şekilde belirtilecek.

## Olası araçlar

- `waybar`: üst çubuk ve modüller
- `wofi` veya `bemenu`: uygulama başlatıcısı için değerlendirilecek seçenekler
- `playerctl` / MPRIS: medya bilgisi ve kontrolü
- `/proc` ve `/sys`: işlemci, bellek ve ağ sayaçları için uygun arayüzler
- `UPower` veya `/sys/class/power_supply`: pil verileri
- `brightnessctl`: desteklenen ekranlarda parlaklık kontrolü

Bunlar başlangıç adaylarıdır; kuruluma geçildiğinde T480 donanımında gerçekten gerekli ve uyumlu olanlar seçilecek. Her özellik için ayrı bir ağır bağımlılık eklemek yerine mümkün olduğunca basit çözümler tercih edilecek.

## Uygulama sırası

1. ThinkPad T480 edinildiğinde donanımı ve ekran çözünürlüğünü doğrula.
2. Arch Linux ve Sway ortamını kur; temel ağ, ses, parlaklık ve pil erişimini test et.
3. Super tuşuyla açılan sade uygulama başlatıcısını yapılandır ve klavye kullanımını doğrula.
4. Waybar'ın sabit konumunu, yüksekliğini ve koyu temasını oluştur.
5. Sol bölümde CPU, bellek ve anlık ağ hızlarını ekle.
6. Orta bölümde Spotify kontrollerini ve **süre göstergelerinden açıkça ayrılmış saati** yerleştir.
7. Sağ bölümde bağlantı, pil, parlaklık ve çalışma alanlarını ekle.
8. Ağ ve pil ayrıntı panellerini ekle.
9. Kaynak tüketimini, okunabilirliği, uzun parça adlarını ve eksik donanım verilerini test et.
10. Kurulum notlarını ve yapılandırmaları bu depoda güncelle.

## Tasarım ilkeleri

- Önce işlevsellik, sonra görsel ince ayar.
- Sabit ve tutarlı yerleşim; gereksiz animasyon yok.
- Düşük bellek ve işlemci tüketimi.
- Gereksiz servis ve bağımlılıklardan kaçınma.
- Klavye merkezli kullanım ve hızlı uygulama erişimi.
- Anlık hız, toplam sayaç, saat ve müzik süresi gibi farklı kavramları görsel olarak ayırma.
- Donanımın sunmadığı verileri varmış gibi göstermeme.
- Proje notlarını ve açıklamalarını Türkçe tutma.

## Durum

**Aşama:** Fikir ve tasarım notları  
**Uygulama:** ThinkPad T480 ve Arch Linux kurulumu hazır olduğunda başlayacak
