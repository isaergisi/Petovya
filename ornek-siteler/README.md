# Örnek siteler: Denizli pilotu

Denizli'de kendine ait web sitesi olmayan beş veteriner kliniği için hazırlanmış, tek dosyalık örnek siteler. Her biri yalnızca **doğrulanmış bilgilerle** yazıldı ve klinik onay vermeden yayına alınmamak üzere işaretlendi. Sayfalarda `noindex` etiketi ve en üstte "Örnek tasarım" şeridi var.

Bilgiler 24 Kasım 2026'da toplandı. Kaynaklar: Google Haritalar kayıtları, Denizli Veteriner Hekimleri Odası listesi ve kliniklerin kendi sosyal hesapları.

## Siteler

| Klinik | Dosya | Kişilik | Yazı tipleri | Hero etkileşimi |
|---|---|---|---|---|
| Vetripol Veteriner Kliniği (Yenişafak, Merkezefendi) | [`vetripol/index.html`](vetripol/index.html) | Sakin, sabırlı, anlatan | Fraunces + Figtree | İmleci izleyen, dokununca yavaşça göz kırpan kedi |
| Hiera Veteriner (Gerzele, Merkezefendi) | [`hiera/index.html`](hiera/index.html) | Modern, titiz, takipçi | Instrument Serif + Schibsted Grotesk | Pamukkale travertenleri: dokununca su aşağı akar |
| Cimihav Veteriner Muayenehanesi (Selçukbey, Merkezefendi) | [`cimihav/index.html`](cimihav/index.html) | Mahalle veterineri, sıcak ve esprili | Bricolage Grotesque + Instrument Sans | Duvardaki köpek ve kedi: dokununca "Hav!" ve "Miyav." |
| PetPlus Veteriner Kliniği (İstiklal, Pamukkale) | [`petplus/index.html`](petplus/index.html) | Düzenli, enerjik | Archivo (geniş kesim) | "Klinikte / Evde" anahtarı, çizim klinikten eve dönüşür |
| Denizli Yenişehir Koşuyolu Veteriner Kliniği (Merkezefendi) | [`kosuyolu/index.html`](kosuyolu/index.html) | Hızlı, kapsamlı, güven veren | Red Hat Display + Red Hat Text | "Şu an acil bir durum mu var?" sorusu: Evet → arama adımları, Hayır → WhatsApp randevusu |

### Önizleme

Dosyalar tek başına çalışır, tarayıcıda doğrudan açılabilir. Depo herkese açık olduğu için GitHub üzerinden şu bağlantılarla da önizlenebilir. Bağlantılar dal `main`'e birleştikten sonra geçerli olur:

- https://raw.githack.com/isaergisi/Petovya/main/ornek-siteler/vetripol/index.html
- https://raw.githack.com/isaergisi/Petovya/main/ornek-siteler/hiera/index.html
- https://raw.githack.com/isaergisi/Petovya/main/ornek-siteler/cimihav/index.html
- https://raw.githack.com/isaergisi/Petovya/main/ornek-siteler/petplus/index.html
- https://raw.githack.com/isaergisi/Petovya/main/ornek-siteler/kosuyolu/index.html

## Her sayfada olanlar

- En üstte "Hemen Ara" ve "WhatsApp'tan Yaz". Mobilde bu iki buton kaydırırken ekranın üstünde kalır.
- Hizmetler, hekim ya da ekip, acil durum kutusu, ulaşım ve çalışma saatleri bölümleri.
- Google Haritalar yol tarifi ve kayıt bağlantısı. Harita, ziyaretçi "Haritayı göster" deyince yüklenir.
- Tarihiyle birlikte gerçek Google puanı ve yorum sayısı. Yorum alıntıları birebir, kısaltılan yerlerde "…" var.

Sayfalarda olmayanlar: sahte yorum, fotoğraf (stok ya da üretilmiş), fiyat, "en iyi" gibi üstünlük iddiaları ve **doğrulanmamış "24 saat açık" ya da "7/24" ifadesi**. Saati bilinmeyen kliniklerde "Gelmeden önce arayın" cümlesi ve kesik çizgili "klinikle netleştirilecek" etiketi var. Çizimler bu iş için çizilmiş özgün SVG'ler. Simgeler Lucide (ISC) ve Simple Icons (CC0), yazı tipleri Google Fonts (OFL).

## Doğrulama özeti

| Klinik | Google (24.11.2026) | Maps'te "Web sitesi" | Hekim adı sitede |
|---|---|---|---|
| Vetripol | 5,0 · 39 yorum | Boş | Yok (bilinmiyor) |
| Hiera | 4,9 · 35 yorum | Boş | Erhan Orhan (oda kaydı, yorumlarda "Erhan Bey") |
| Cimihav | 4,9 · 37 yorum | Boş | Mücahit Aşan (oda kaydı ve telefon eşleşiyor) |
| PetPlus | 4,8 · 16 yorum | Boş | Yok (kayıt ve yorumlardaki adlar uyuşmuyor) |
| Koşuyolu | 4,9 · 49 yorum | Instagram hesabı | "Savaşkan Bey" (yorumlardan, soyadı yok) |

İlk listedeki Gaia (gaiavetpol.com) ve Merlinvet (Wix alt alan adı) siteleri olduğu için, yedek aday Merkez Veteriner de (denizlimerkezveteriner.com) aynı nedenle çıkarıldı. Ayrıntılı rapor proje dosyalarında: `pilot/Denizli pilot klinikleri web doğrulama.md`.

## Yayından önce klinikle teyit edilecekler

| Klinik | Teyit |
|---|---|
| Hepsi | Numara WhatsApp'ta mı? Değilse WhatsApp butonu SMS'e çevrilir. Puan ve yorum sayısı yayın günü yeniden okunur. |
| Vetripol | Hekim adı. Çalışma saatleri (Maps'te "24 saat açık" yazıyor, doğrulanmadı). |
| Hiera | Güncel telefon: Maps'te 0537 438 39 96, oda kaydında 0553 256 39 96. Kapanış saati 19:00 mı, 17:00 mi? (Google'da iki tablo var, sitede 19:00 tablosu kaynak notuyla gösteriliyor.) |
| Cimihav | Gece ya da 24 saat hizmet var mı? |
| PetPlus | Sitede hangi hekim adları yer alacak? Ev ziyareti düzenli bir hizmet mi? Tanıtım mesajında ve sitede yorumlarla ilgili hiçbir tartışmaya girilmemeli. |
| Koşuyolu | Hekimin tam adı. "7/24 acil" yazılı olarak teyit edilirse saat satırına eklenir. Oda kaydındaki resmi unvan. |

## Kontrol

Beş sayfa, Playwright ile 1440×900, 1024×768, 768×1024 ve 390×844 boyutlarında, ayrıca JavaScript kapalıyken kontrol edildi. Sonuçlar:

- Yatay taşma yok.
- 44 px'den küçük dokunma hedefi yok.
- Konsolda hata yok.
- Fontlar yükleniyor.
- Mobil eylem çubuğu kaydırınca üstte kalıyor.
- `prefers-reduced-motion` açıkken animasyonlar kapanıyor.

Tasarım sistemi, tokenlar ve etkileşim ayrıntıları için [HANDOFF.md](HANDOFF.md).
