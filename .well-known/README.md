# `.well-known` — uygulama linki doğrulaması

Bu klasör **Avare**'nin davet linkini (`/avare/join/?code=ABC12`) kurulu
uygulamada açabilmesi için gereken doğrulama dosyalarını taşır. Eklendi:
2026-08-25.

`.nojekyll` repo kökünde duruyor, yani GitHub Pages bu klasörü olduğu gibi
servis eder. İki dosya da **düz metin, `Content-Type` önemli değil** (Apple
`application/json` istemiyor artık, uzantısız dosya yeterli).

---

## ⚠️ `assetlinks.json` — EKSİK PARMAK İZİ VAR

Şu an dosyada **yalnızca yükleme (upload) anahtarının** SHA-256 parmak izi
yazılı:

```
1D:0F:CB:B7:79:70:FC:08:A9:72:EF:19:10:DF:89:62:46:35:0C:69:A6:85:1D:9F:5F:96:C6:A2:B9:E4:11:C9
```

Bu, **Play'den kurulan sürümler için YETMEZ.** Google Play App Signing
uygulamayı kendi anahtarıyla yeniden imzalıyor; Android doğrulamayı o
sertifikanın parmak iziyle yapar.

**Yapılacak:** Play Console → *Test and release* → *App integrity* →
*App signing key certificate* → **SHA-256 certificate fingerprint** değerini
kopyala ve `sha256_cert_fingerprints` dizisine **ikinci eleman olarak** ekle
(yükleme anahtarınınkini silme — o, yerel/dahili test kurulumları için
lazım).

Doğrulamayı kontrol:

```
https://digitalassetlinks.googleapis.com/v1/statements:list?source.web.site=https://heyisoft.github.io&relation=delegate_permission/common.handle_all_urls
```

Cihazda: `adb shell pm get-app-links com.heyisoft.avare` → `verified`
görmelisin.

---

## `apple-app-site-association`

`MTN6ZG2P72.com.heyisoft.avare` + `/avare/join*` yazılı, ek işlem gerekmiyor.

**Ama repo dışında bir adım var:** Apple Developer portalında App ID'de
**Associated Domains** capability'si açık olmalı ve provisioning profile
yenilenmeli. Açık değilse imzalama *"provisioning profile doesn't include
com.apple.developer.associated-domains"* der.

Doğrulama, uygulama kurulduktan sonra Apple'ın CDN'inden yapılır; dosyayı
değiştirdikten sonra yayılması birkaç saat sürebilir.

---

## Doğrulama olmazsa ne olur?

Akış **kırılmaz**. Link tarayıcıda açılır ve `/avare/join/` sayfası davet
kodunu gösterip mağazaya yönlendirir; paylaşılan mesaj zaten kodu da
taşıyor. Yani bu klasör linki *hızlandırır*, akışın ön şartı değildir.
