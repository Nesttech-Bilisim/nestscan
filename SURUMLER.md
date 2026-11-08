# NestScan sürümleri

Her sürümde neyin değiştiği. Kullandığınız sürüm, NestScan penceresinin alt çubuğunda yazar.
İndirme: https://github.com/Nesttech-Bilisim/nestscan/releases/latest

## 2.0 · 7 Kasım 2026

- **Tür kutusu düzeltildi:** "TypeOption { Type = … }" gibi kod yerine şu anki tür yazar (ör. "Sunucu").
- **Kendi türünü yazma:** tür kutusu artık yazılabilir. Listeden seçilir ya da yeni bir tür yazılıp **Enter**'a basılır
  (ör. "Hipervizör", "Santral", "Saat cihazı"). Yazılan tür:
  - cihazın MAC adresine göre hatırlanır, sonraki taramalarda uygulanır;
  - diğer cihazların listesinde de çıkar; filtre şeridine kendi düğmesiyle eklenir;
  - liste, PDF/Excel raporu ve geçmişte görünür.
  Standart bir türün adı yazılırsa (büyük/küçük harf, Türkçe harf fark etmez: "sunucu", "NAS") o tür seçilir.
  "Otomatik (…)" ile geri alınır; Esc yazılanı iptal eder. En fazla 32 karakter.
- **vCenter:** web başlığı JavaScript ile dolan ('" + ID_VC_Welcome + "') vCenter artık **VMware vCenter** adıyla,
  Sunucu türünde görünür. Bu tür kod parçası başlıklar hiçbir cihazda ad olarak kullanılmaz.
- Seagate Cloud Systems / Dot Hill depolama cihazları NAS sayılır.

## 1.9 · 7 Kasım 2026

- **Türü elle değiştirme:** detay panelinde "TÜR" açılır kutusu. Yanlış tanınan cihazın türü seçilir; seçim cihazın
  MAC adresine göre hatırlanır ve sonraki taramalarda (aynı cihaz) uygulanır. "Otomatik (…)" ile geri alınır.
  Seçimler `%LOCALAPPDATA%\NestScan\cihaz-turleri.json` dosyasındadır (yalnız MAC → tür; şifre yok).
- **VMware ESXi tanıma:** ESXi'nin MAC'i fiziksel ağ kartınındır (Broadcom, HPE, Intel), üreticiden anlaşılmaz.
  Artık HTTPS sertifikasındaki "VMware" bilgisinden, Host Client sayfasından ya da **902 portundan** (VMware
  yetkilendirme servisi, varsayılan port listesine eklendi) tanınır: tür **Sunucu**, ad **VMware ESXi**.
  vCenter, Proxmox, HPE iLO, Dell iDRAC, Lenovo XClarity de tanınır; detay panelinde "Yazılım" satırı.
  Ayarlardaki port listesi değiştirilmemişse 902 kendiliğinden eklenir.
- **Switch tanıma:** web paneli "ARUBA - Login Form" olan Aruba switch'ler ve OfficeConnect, ProCurve, Cisco SG/CBS,
  Netgear ProSAFE/GS, D-Link DGS, TP-Link JetStream/TL-SG, Zyxel, Ruijie RG-S, H3C… başlıklı cihazlar ile SW-…,
  CORE-SW…, USW-… adlı cihazlar **Ağ cihazı** olur ve "Aruba switch" gibi adlandırılır. Aruba Instant erişim
  noktaları erişim noktası kalır.
- Windows adı olmayan cihazlarda web paneli DNS adı olsa da okunur (tür tanıma için; ad yine DNS'ten).

## 1.8 · 7 Kasım 2026

- **Yeni tür: Erişim noktası** (filtre şeridinde, kendi simgesiyle; Ayarlar'da çift tık tercihi). SSH açık olduğu için
  "Sunucu" görünen erişim noktaları artık doğru tanınır:
  - **Aruba Instant:** MAC'i "Hewlett Packard Enterprise" görünse de sertifikadaki `securelogin.arubanetworks.com`'dan.
  - **Ruijie / Reyee, Ruckus, Cambium, EnGenius, Aerohive, Mist:** üreticiden (aynı markanın switch'leri hariç:
    RG-S…, ES…, "switch" adlılar ağ cihazı kalır).
  - **TP-Link EAP (Omada):** web başlığından ya da EAP… adından (TP-Link modem/switch ağ cihazı kalır).
  - **UniFi:** Ubiquiti MAC'li ve yalnız SSH açık (web paneli olmayan) cihazlar.
  - **Adından:** AP-OFIS, KAT2-AP, AP01, UAP…, U6-…, RG-RAP…, IAP…, WAP…; dosya paylaşımı/RDP açıksa bilgisayar sayılır.
  - Ağ geçidi her zaman ağ cihazıdır. HP iLO (ILOCZ…) sunucu kalır.
- **Daha iyi adlar:** sertifikadaki "securelogin", "login", "www" gibi genel adlar ad sayılmaz; markadan ad verilir:
  "Aruba erişim noktası", "TP-Link erişim noktası". Geçmiş kayıtlarına marka da yazılır.

## 1.7 · 7 Kasım 2026

- **NAS tanıma:** QNAP cihazları "Bilgisayar" görünüyordu (SMB/445 açık olduğu için). QNAP'ın MAC kaydı
  "ICP Electronics" adıyla geçer; bu üretici artık NAS sayılır. Üretici bilinmese de adı NAS'ı gösteren cihazlar
  NAS olur: QNAP'ın varsayılan adı (NAS + MAC'in son 6 hanesi, ör. NASC12322), NAS-…, NAS01, Synology DS920,
  QNAP TS-453, DiskStation, TrueNAS, ReadyNAS, MyCloud. NAS kontrolü bilgisayar, kamera ve ağ cihazından önce yapılır.
  Çift tıkta NAS'ın web paneli açılır. NASA-PC gibi adlar NAS sayılmaz.

## 1.6 · 7 Kasım 2026

- **Tek kurulum dosyası, iki seçenek:** `NestScan-1.6-Kurulum.exe` açılınca "İşlemi seçin" sayfası gelir:
  - **Kurun:** bilgisayara kurar (Başlat menüsü, masaüstü kısayolu, Denetim Masası'ndan kaldırma). İleri
    yerine doğrudan **Kur** düğmesi çıkar; klasör ve kısayol seçmek için "Gelişmiş ayarlar" işaretlenir.
  - **Çalıştır:** kurmadan açar. Dosyalar kullanıcının geçici klasörüne (`%TEMP%\NestScan-1.6`) açılır ve NestScan
    hemen başlar; kaldırıcı, Programlar kaydı ve kısayol oluşturulmaz. Müşteride tek seferlik tarama için.
- Kurulum sihirbazının sağ üstünde NestScan simgesi; açılıştaki "tüm kullanıcılar / yalnız ben" sorusu kaldırıldı
  (tüm kullanıcılar için kurmak gerekirse: `NestScan-1.6-Kurulum.exe /ALLUSERS`).
- Taşınabilir zip yine üretilir (USB'den çalıştırmak için).

## 1.5 · 7 Kasım 2026

- **Adsız cihazlar:** NetBIOS ya da DNS adı olmayan cihazlarda web panelinin sayfa başlığı ve HTTPS sertifikasındaki
  ad okunur (ör. "Sophos Firewall - Login" → **Sophos Firewall**). Bu da yoksa üreticiden ve türden ad verilir:
  "Sophos ağ geçidi", "HP yazıcı", "Hikvision kamera". "İsimsiz cihaz" yalnız hiçbir bilgi yoksa kalır.
  Tahmini adlar soluk yazılır; ayrıntı panelinde "Web başlığı" ve "Sertifika" satırları görünür.
  Ayarlar › Tarama'dan kapatılabilir. FortiGate, pfSense, OPNsense, RouterOS, UniFi adları ağ cihazı sayılır.
- **Sayı kutuları tıklanabilir:** "Bulunan cihaz", "Yeni cihaz", "Uzak masaüstü açık", "Web yönetim paneli"
  kutusuna tıklayınca liste o cihazlara süzülür; aynı kutuya tekrar tıklayınca filtre kalkar.
  Filtre şeridine "Uzak masaüstü" ve "Web paneli" eklendi.
- **Tam ekran düzeltmesi:** küçük ya da yüksek ölçekli ekranlarda (ör. 1366×768 %125–150, RDP oturumu)
  tam ekranda pencere sağdan taşıyor, kapat/küçült/büyüt düğmeleri görünmüyordu. Pencerenin en küçük boyutu
  artık bulunduğu ekranın çalışma alanını aşmaz, ilk açılış boyutu ekrana sığdırılır; dar ekranlarda
  doğrudan tam ekran açılır. Ekran ya da ölçek değişince yeniden ayarlanır.

## 1.4 · 4 Kasım 2026

- **Kurulum paketi:** `Paket-Olustur.cmd` (ya da `tools\build-release.ps1`) tek komutla üretir:
  - `NestScan-1.4-Kurulum.exe`: Türkçe kurulum sihirbazı; yönetici yetkisi istemez; Başlat menüsü ve
    isteğe bağlı masaüstü kısayolu; Denetim Masası'ndan kaldırılır, kaldırırken geçmiş/ayarlar silinsin mi diye sorar.
  - `NestScan-1.4-Tasinabilir.zip`: kurulumsuz, klasörden ya da USB'den çalışır.
  - İkisinde de .NET gömülüdür; müşteri bilgisayarına ayrıca bir şey kurulmaz.
- Telefon adları (…-S25-Ultra, Galaxy, Pixel, Redmi, iPad…) "Mobil cihaz" olarak tanınır.
- Paket betiği Inno Setup'ı her sürüm klasöründe ve Windows'un program kayıtlarında arar; gerekirse
  `-Iscc "<ISCC.exe yolu>"` verilebilir. `installer\NestScan.iss`, Inno Setup'ta açılıp doğrudan da derlenebilir
  (sürüm numarasını NestScan.exe'den okur).

## 1.3 · 4 Kasım 2026

- **Raporlar:** tarama ekranından ve geçmişten PDF ya da Excel envanter raporu. PDF'te NestScan başlığı,
  firma adı, müşteri, tür özetleri, cihaz tablosu, yeni cihazlar turuncu, görülmeyen cihazlar ayrı tabloda,
  sayfa numaraları. Türkçe karakterler için Windows'un Segoe UI yazı tipi gömülür. Excel'de filtreli
  "Cihazlar", "Özet" ve (varsa) "Görülmeyenler" sayfaları.
- **Geçmiş:** tarama ekranında "Müşteri / konum" alanı; tarama bu adla kaydedilir. Sonraki taramada önceki
  taramaya göre **yeni** (YENİ rozeti, "Yeni" filtresi) ve **görülmeyen** cihazlar gösterilir; IP'si değişen
  cihaz yeni sayılmaz. Geçmiş sayfasında müşteriler, taramaları, fark, rapor, yeniden tara, silme.
  Kayıtlarda yalnız cihaz listesi vardır, şifre yoktur. Ayarlardan kapatılabilir.
- **Ayarlar:** taranacak portlar, ping/port bekleme süreleri, eşzamanlı tarama, DNS/NetBIOS, ping'e kapalı
  cihazlarda port denemesi, cihaz türüne göre çift tıkta açılacak bağlantı, açık/koyu tema, geçmiş kaydı,
  rapordaki firma adı.
- Sol menüde Tarama, Geçmiş, Ayarlar (Raporlar, tarama ve geçmiş ekranlarındaki düğmelere taşındı).
- Tekrarlayıcı rozeti sadeleştirildi; turuncu rozet artık "YENİ" cihaz için.

## 1.2 · 4 Kasım 2026

- Uygulama simgesi: pencere başlığında, görev çubuğunda ve NestScan.exe dosyasında NestScan simgesi.
- MAC adresi okunamayan tekrarlayıcı (ör. RE705X) tarama sonunda adından tanınır; arkasındaki cihazlarda
  yine "RE705X üzerinden bağlı" yazar.

## 1.1 · 4 Kasım 2026

- Çift tıkta **Bağlan penceresi**: RDP ve paylaşımlarda kullanıcı adı + şifre girilir, direkt giriş yapılır.
  SSH'ta yalnız kullanıcı adı sorulur. Web panelleri sormadan açılır. "Kimliksiz aç" seçeneği.
- **Hiçbir kimlik saklanmaz:** kullanıcı adı ve şifre her seferinde yeniden girilir. Windows'a verilen kimlik
  bağlantı kurulunca (en geç 1 dakika) silinir. Uzak Masaüstü'nün kendi tuttuğu "son bağlanılan bilgisayar /
  son kullanıcı adı" kayıtları, NestScan'in eklediği kadarıyla temizlenir (müşterinin önceki kayıtlarına dokunulmaz).
- Liste görünümü: sütun sırası Ad, IP, MAC, …; IP ve MAC açılışta tam görünür, ad sütunu sabit kalır,
  altta yatay kaydırma.
- Bağlan penceresi açılırken çıkan "StaticResourceExtension" hatası düzeltildi.
- Wi-Fi tekrarlayıcının kendisi (ör. TP-Link RE705X) tanınır, arkasındaki cihazlarda "… üzerinden bağlı" yazar.
- Kart adlarının koyu zeminde görünmemesi düzeltildi; Uyandır düğmesi yalnız bilgisayar/sunucu/NAS'ta.

## 1.0 · 3 Kasım 2026

- İlk masaüstü sürümü (WPF): tarama ekranı, kart ve liste görünümü, filtreler, arama, detay paneli.
- Tarama motoru: ping + ARP, NetBIOS/DNS adı, IEEE üretici listesi, 23 port, cihaz türü tahmini,
  tekrarlayıcı arkasındaki cihazların tespiti.
- Çift tıkla açma: Uzak masaüstü, web paneli, Gezgin'de paylaşımlar, SSH. Wake-on-LAN, IP/MAC kopyalama.
