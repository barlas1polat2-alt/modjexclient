# JexClient

BoxPvP odaklı, Dawn Client tarzı istemci-taraflı (client-side) Fabric modu.
Minecraft 1.21 için.

## Bu modda neler var

- Kare kalpler (toggle)
- Envanter HUD (toggle)
- Sis kapatma/açma
- Elytra görünürlük toggle
- Düz zırh (basitleştirilmiş ilk versiyon — bkz. `ArmorFeatureRendererMixin` yorumları)
- Yerdeki item büyüklüğü ayarı (slider)
- IP HUD gösterimi + konum (4 köşe)
- Scoreboard / Bossbar toggle
- Performans modu (FPS boost — görüş mesafesini otomatik düşürür)
- Arkadaş listesi + mod-içi sohbet (arka planda `/msg` komutunu kullanır,
  gelen whisper mesajları normal chat'ten gizlenir, sadece kendi sohbet
  ekranında görünür)
- Menü tuşu: varsayılan olarak Türkçe klavyede **ğ** tuşunun fiziksel
  konumuna atanmıştır (Options > Controls > JexClient > Open Menu'den
  değiştirilebilir)

## ⚠️ Önemli: Bu kodu ben (Claude) derleyemedim

Kodu yazdım ama çalıştığım ortamın internet erişimi Fabric/Mojang
sunucularına kapalı olduğu için `.jar` dosyasını burada üretemedim.
Bunun yerine **GitHub Actions** ile otomatik derleme kurulu — sen sadece
kodu GitHub'a yükleyeceksin, gerisini GitHub'ın sunucuları yapacak.

## Kurulum — Tek Seferlik (5 dakika)

1. https://github.com adresinde ücretsiz hesap aç (yoksa).
2. Sağ üstten **New repository** ile yeni, **boş** bir repo oluştur
   (örn. adı: `jexclient`). "Add a README" kutusunu **işaretleme**.
3. Bu klasördeki (indirdiğin zip'i açtığında çıkan) **tüm dosyaları**
   sürükle-bırak ile GitHub'daki repo sayfasına yükle:
   - Repo sayfasında **Add file > Upload files** butonuna tıkla
   - Zip'i açtığın klasördeki her şeyi (`.github` klasörü dahil, gizli
     klasör görünmüyorsa dosya gezgininde "gizli dosyaları göster"i aç)
     sürükle
   - Alt kısımda **Commit changes** de
4. Yükleme bitince otomatik olarak **Actions** sekmesinde bir derleme
   başlayacak (birkaç dakika sürer, sarı nokta > yeşil tik olunca biter).
5. Derleme bitince repo ana sayfasında sağ tarafta **Releases** bölümüne
   tıkla, en üstteki (**latest**) release'e gir, oradaki `.jar` dosyasına
   tıklayıp indir.
6. İndirdiğin `jexclient-1.0.0.jar` dosyasını (sources.jar olanı DEĞİL)
   `.minecraft/mods` klasörüne koy.
7. Minecraft'ı **Fabric Loader 1.21** profiliyle başlat (Fabric yüklü
   değilse önce https://fabricmc.net/use/installer/ adresinden Fabric
   Installer ile 1.21 için Fabric'i kur), ayrıca `fabric-api` modunu da
   (Modrinth/CurseForge'dan indirip) mods klasörüne ekle — JexClient buna
   ihtiyaç duyuyor.

Bundan sonra ben kodda değişiklik/ekleme yaptığımda, sen sadece güncellenen
dosyaları tekrar aynı şekilde GitHub'a yüklersin, yeni jar otomatik
Releases sayfasında belirir.

## Eğer derleme (Actions) kırmızı çarpı ile başarısız olursa

Bu normal olabilir — Minecraft'ın iç kod isimleri (Yarn mappings) sürüm
sürüm ufak değişebiliyor ve ben burada gerçek derleme yapamadığım için
bazı mixin metod adları tam tutmayabilir (özellikle `InGameHudMixin`,
`ElytraFeatureRendererMixin`, `ArmorFeatureRendererMixin`,
`ItemEntityRendererMixin` içindekiler — kod içinde bununla ilgili yorumlar
bıraktım).

Yapman gereken tek şey: **Actions** sekmesinde kırmızı çarpılı derlemeye
tıkla, "Build with Gradle" adımındaki kırmızı hata metnini kopyala, bana
buraya yapıştır — ben de doğru metod adıyla düzeltip sana güncel dosyayı
veririm.

## Notlar

- Bu mod tamamen **client-side**'dır, sunucu tarafında bir şey yapmaz.
- Arkadaş sohbeti gerçek bir "özel protokol" değildir; sunucunun `/msg`
  (bazı sunucularda `/w` ya da `/tell`) komutunu kullanır. Eğer bağlandığın
  sunucuda whisper komutu farklıysa `FriendManager.sendMessage()` içindeki
  komut adını değiştirmen (veya bana söylemen) yeterli.
- BoxPvP sunucuları genelde anti-cheat kullanır; bu mod **hile (fly, kill
  aura, reach vb.)** içermez, sadece görsel/HUD/performans ayarlarıdır —
  yine de kullanmadan önce sunucunun mod kurallarını kontrol et.
