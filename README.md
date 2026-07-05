# Sinyal — Masaüstü Uygulaması

Bu, web sitenizi (`https://sohbet.xivizley.xyz`) kendi penceresinde açan, gerçek
bir masaüstü uygulaması. Tarayıcı çubuğu yok, görev çubuğunda/dock'ta kendi
ikonu var, ayrı bir uygulama gibi çalışıyor.

## Yerelde test etmek (kendi bilgisayarında)

```bash
npm install
npm start
```

Bu, Electron'u açar ve doğrudan `sohbet.xivizley.xyz`'i yükler. Değişiklik
yapman gerekirse `main.js` içindeki `APP_URL` değişkenini güncelle.

## Windows / Mac / Linux için kurulum dosyası üretmek

### Yöntem 1 — GitHub Actions (ÖNERİLEN, üçünü de otomatik üretir)

Mac uygulamasını güvenilir şekilde derlemek için bir Mac'e ihtiyaç var —
GitHub Actions bunu senin için ücretsiz bir Mac/Windows/Linux sunucusunda
otomatik yapar. Adımlar:

1. GitHub'da yeni, boş bir repo oluştur (örn. `sinyal-desktop`)
2. Bu klasörün içeriğini o repo'ya push et:
   ```bash
   cd sinyal-desktop
   git init
   git add .
   git commit -m "İlk sürüm"
   git branch -M main
   git remote add origin https://github.com/KULLANICI_ADIN/sinyal-desktop.git
   git push -u origin main
   ```
3. Bir "tag" (sürüm etiketi) oluşturup push et — bu, otomatik derlemeyi tetikler:
   ```bash
   git tag v1.0.0
   git push origin v1.0.0
   ```
4. GitHub'da repo sayfasında **Actions** sekmesine git, "Masaüstü Uygulamasını
   Derle" işleminin çalıştığını göreceksin (birkaç dakika sürer)
5. Bittiğinde repo sayfanın sağındaki **Releases** bölümüne git — `v1.0.0`
   adında bir sürüm otomatik oluşmuş olacak, altında Windows/Mac/Linux
   dosyaları hazır ve **kalıcı** indirme linkleriyle duruyor. Bu linkleri
   direkt WordPress sayfana koyabilirsin, örneğin:
   ```
   https://github.com/KULLANICI_ADIN/sinyal-desktop/releases/download/v1.0.0/Sinyal-Setup-1.0.0.exe
   ```

Elle tetiklemek istersen (tag oluşturmadan): Actions sekmesinde soldan
"Masaüstü Uygulamasını Derle" seçip **"Run workflow"** butonuna basman yeterli.

### Yöntem 2 — VDS'inde yerel derleme (sadece Linux için garantili)

```bash
npm install
npm run build:linux
```

`dist/` klasöründe `.AppImage` ve `.deb` dosyaları oluşur. Windows derlemesini
de (`npm run build:win`) Linux üzerinde `wine` kurarak deneyebilirsin ama
bazen sorun çıkarabilir — GitHub Actions daha güvenilir.

**Mac derlemesini VDS'te (Linux) yapma** — imzalanmamış, güvenilmez bir
paket çıkar ve genelde çalışmaz. Yöntem 1'i kullan.

## Uygulama ne yapıyor, ne yapmıyor

- Web sitenle birebir aynı şeyi gösterir (mesajlaşma, sesli/görüntülü arama,
  ekran paylaşımı — hepsi web'deki gibi çalışır, çünkü aynı sayfayı açıyor)
- İnternet bağlantısı hâlâ gerekli (veriler hep sunucundan geliyor)
- Masaüstü bildirimleri, tray ikonu gibi ek özellikler şu an yok — istersen
  sonra ekleyebiliriz

## İkonu değiştirmek

`icon.png` dosyasının üzerine kendi logonu (512x512 piksel, PNG) koy, sonra
tekrar derle.
