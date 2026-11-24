# Tasarım devri: Denizli örnek siteleri

Bu belge, `ornek-siteler/` altındaki beş tek dosyalık sayfanın geliştiriciye devri içindir. Beş site **tek bir tasarım sistemini** paylaşır, her klinik bu sistemin üstüne kendi palet, yazı tipi ve kişiliğini koyar. Önce ortak sistem anlatılıyor, sonra klinik klinik farklar.

Kaynak dosyalar: `vetripol/`, `hiera/`, `cimihav/`, `petplus/`, `kosuyolu/` klasörlerindeki `index.html`. Hepsi satır içi CSS ve JS içerir. Dış bağımlılık olarak yalnızca Google Fonts kullanılır. Harita ise kullanıcı isterse Google'dan yüklenir.

---

## 1. Ortak sistem

### Genel bakış

Sayfayı açan kişi çoğunlukla telefondan, çoğu zaman da endişeli biri. Bu yüzden her sayfanın ilk işi aramayı ve WhatsApp'ı tek dokunuşa indirmek. İkinci işi "Acil durumda ne yapmalı?" sorusuna sakin bir cevap vermek. Bölüm sırası her sitede aynı:

1. **Hero**: h1, kısa açıklama, doğrulanmış Google puanı, telefon ve bir hatırlanacak etkileşim
2. **Hizmetler**
3. **Hekim / ekip**: puan kartı ve birebir yorum alıntıları
4. **Acil durum kutusu**
5. **Ulaşım**: adres, saatler, yol tarifi, isteğe bağlı harita
6. **Alt bilgi**: kaynak ve lisans satırı

### Yerleşim

| Öğe | Değer | Neden |
|---|---|---|
| `.wrap` | `max-width: calc(var(--maxw) + 2 * var(--gutter))`, yatay padding `var(--gutter)` | Sol ve sağ içerik kenarları her bölümde aynı çizgide |
| `--gutter` | `clamp(16px, 5vw, 56px)` (Hiera: 64px üst sınır) | 390 px'de 16 px yan boşluk |
| `--maxw` | 1180 ile 1200 px | Satır uzunluğu okunur kalsın |
| Izgara | 12 sütun, `gap: clamp(24px, 4vw, 56px)` | Bölümler 5+7 ya da 6+6 bölünür |
| Bölüm | `main > section`, `min-height: calc(100svh - var(--header-h))`, `padding-block: clamp(56px, 9vh, 104px)`, içerik dikeyde ortalı | Her bölüm bir ekran, bol boşluk |
| `scroll-margin-top` | `var(--header-h)` | Menü bağlantıları başlığın altına sakladırmaz |

### Ortak tokenlar

Her sitenin `:root` bloğu aynı adlarla başlar. Değerler ikinci bölümdeki tablolarda.

| Token | Görev |
|---|---|
| `--bg` / `--paper` / `--cream` | Sayfa zemini |
| `--surface` / `--white` | Kart zemini |
| `--ink` | Ana metin ve koyu yüzeyler |
| `--muted` | İkincil metin (zemin üstünde en az 4.5:1 kontrast) |
| `--accent` (ve `-2`, `-hi`) | Birincil eylem, vurgu kelimesi |
| `--line` | Kart kenarları, ayırıcılar |
| `--wa` `#1FAF55` | Yalnızca WhatsApp simgesinin rengi; buton zemininde kullanılmaz |
| `--font-display`, `--font-body` | Başlık ve gövde yazı tipleri (PetPlus tek aile: `--font`) |
| `--r-s`, `--r-m`, `--r-l` | Köşe yarıçapları: buton, küçük kart, büyük kart |
| `--header-h` | Masaüstünde 72 ile 76 px, mobilde 60 ile 62 px |
| `--ease` | Tüm geçişlerin eğrisi, `cubic-bezier(.2,.7,.2,1)` ailesi |

### Tipografi ölçeği

| Rol | Boyut | Not |
|---|---|---|
| h1 | `clamp(2.6rem, 6vw, 5.2rem)` civarı, satır yüksekliği 1.0 ile 1.05 | Vurgu kelimesi italik ya da `--accent` renginde |
| h2 (`.h2`) | `clamp(2.1rem, 4.6vw, 3.6rem)` | Her bölüm bir h2 ile başlar |
| Giriş metni (`.lead`) | `clamp(1.075rem, 1.5vw, 1.2rem)`, `max-width: 50–52ch` | `--muted` renginde |
| Gövde | `1.0625rem` (17 px), satır yüksekliği 1.6 | Mobilde de 16 px altına inilmez |
| Küçük not | `.8125rem` ile `.875rem` | Kaynak ve teyit notları |

### Ortak bileşenler

| Bileşen | Varyant | İçerik | Not |
|---|---|---|---|
| Üst çubuk `.top` | — | Logo, menü, `.actions` | `position: sticky`. Mobilde iki satır olur, `top` değeri logo satırının yüksekliği kadar eksi verilir (−56 ya da −58 px). Böylece kaydırınca yalnızca buton satırı ekranda kalır |
| Eylem butonu `.btn` | `call` (birincil), `wa` (ikincil), `line` (çerçeve), site özel | Simge + fiil + nesne: "Hemen Ara", "WhatsApp'tan Yaz", "Yol tarifi al" | `min-height: 48px`, simge 20 px |
| Puan çipi | Hero'da | "4,9 ★★★★★ 49 Google yorumu" | Google Maps kaydına (`?cid=`) bağlanır |
| Puan kartı | Hekim bölümünde | Büyük puan, yıldızlar, yorum sayısı bağlantısı, tarih notu | "24 Kasım 2026'da Google Haritalar'dan alındı" notu zorunlu |
| Yorum alıntısı | — | `<q>` + `<cite>` ("Ad S., Google yorumu") | Metin birebir. Kısaltma yalnızca `…` ile yapılır, kelime eklenmez |
| Acil durum kutusu | — | h2, kısa paragraf, arama butonu, "hemen arayın" listesi, "yola çıkmadan önce" sıralı listesi, genel bilgi notu | İçerik beş sitede aynı tıbbi çekirdeği taşır, ton siteye göre değişir |
| Saat satırı | `data-confirm="hours"` | "Gelmeden önce arayın…" ve kesik çizgili teyit çipi | Saat doğrulanınca çip kaldırılır ve gerçek saat yazılır. Hiera'da doğrudan Google'daki saat tablosu var |
| Harita kutusu `#map` | Kapalı / açık | Kapalıyken simge, gizlilik notu, "Haritayı göster" butonu | Tıklanınca `iframe` eklenir. O ana kadar Google'a istek gitmez |
| Örnek şeridi `.sample-note` | — | "Örnek tasarım… klinik onayı olmadan yayına alınmaz." | Yayında silinir |

### Durumlar ve etkileşimler

| Öğe | Durum | Davranış |
|---|---|---|
| `.btn` | Hover | `translateY(-2px)` ve yumuşak gölge, 160 ms |
| `.btn` | Basılı (`:active`) | `scale(.97)`, gölge yok |
| `.btn` | Odak | 3 px `--accent` çerçeve, 3 px boşluk (`:focus-visible`) |
| Menü bağlantısı | Hover | Alt çizgi soldan sağa çizilir (`background-size` 0 → 100%), 250 ms |
| Bağlantılı çip ve kart | Hover | `translateY(-2px)` |
| Harita butonu | Tık | Kapak kaldırılır, `iframe` `loading="lazy"` ve erişilebilir `title` ile eklenir |
| Butonlarda devre dışı ya da yükleniyor durumu | — | Yok: hiçbir buton ağ isteği beklemiyor. Form eklenirse bu durumlar tanımlanmalı |

### Duyarlı davranış

| Kırılma | Değişen |
|---|---|
| 1180 px ve üstü | Tam düzen: üst çubukta menü ve iki buton, 5+7 / 6+6 ızgaralar |
| 1179 px ve altı | Menü gizlenir, butonlar sağa yaslanır. 1024 px'de menü iki satıra kırılıyordu, bu yüzden erken gizleniyor |
| 1023 px ve altı | Izgaralar tek sütuna iner. Kart ızgaraları iki sütun olur |
| 899 px ve altı | Yalnızca Vetripol: hero kedisi metnin altına iner |
| 759 px ve altı | Mobil: üst çubuk iki satır olur ve buton satırı yapışkan kalır. Bölümler `min-height: auto`, dikey boşluk 64 px. Kartlar tek sütun olur, eylem butonları tam genişlik |

Neden: Ziyaretçilerin çoğu telefondan geliyor ve aramayı başparmakla yapıyor. Bu yüzden iki eylem mobilde her zaman ekranın üstünde ve yan yana, her biri en az 48 px yüksekliğinde.

### Hareket

| Öğe | Tetik | Animasyon | Süre | Eğri |
|---|---|---|---|---|
| Hero metni `[data-enter] > *` | Sayfa yüklenince (`html.is-ready`) | `opacity 0 → 1`, `translateY(16–18px) → 0`, çocuklar arasında 80 ms gecikme | 700–800 ms | `--ease` |
| Hero görseli | Sayfa yüklenince | Ölçek ya da kayma ile belirme, 200–350 ms gecikmeli | 800–1000 ms | `--ease` |
| Hover adımları | Hover | Bkz. durum tablosu | 160–250 ms | `--ease` |
| Bölüm anı (siteye özel) | Görünür alana girince, bir kez (`IntersectionObserver`) | Bkz. ikinci bölüm | 900–1200 ms | `--ease` |

`prefers-reduced-motion: reduce` açıkken tüm animasyon ve geçişler kapanır, giriş öğeleri doğrudan görünür, imleç takibi ve otomatik oynatma çalışmaz.

### Erişilebilirlik

- `lang="tr"`, ilk odaklanan öğe "İçeriğe geç" bağlantısı.
- Odak sırası şöyle: içeriğe geç, logo, menü, Hemen Ara, WhatsApp'tan Yaz, hero etkileşimi, bölümler sırayla, alt bilgi.
- Tüm dokunma hedefleri en az 44 × 44 px. 390 px'de Playwright ile ölçüldü, küçük hedef yok.
- Dekoratif SVG'ler `aria-hidden="true"`. Etkileşimli SVG'ler (Cimihav'daki köpek ve kedi) `role="button"`, `tabindex="0"` ve `aria-label` taşır, Enter ve Boşluk ile çalışır.
- Durum değiştiren butonlar (PetPlus anahtarı, Koşuyolu acil sorusu) `aria-pressed` taşır. Değişen içerik `aria-live="polite"` bölgede.
- Yalnızca görsel olan büyük kelimeler ("Yenişafak", "Neredeyiz?") `aria-hidden`. Asıl bilgi hemen altındaki h2'de.
- Puan çiplerinde yıldızlar `aria-hidden`, sayı ve yorum adedi `aria-label` ile okunur.

### Uç durumlar

- **Saat bilinmiyor:** Saat yazılmaz. "Gelmeden önce arayın" cümlesi ve teyit çipi gösterilir. "24 saat açık" ifadesi klinik yazılı olarak teyit etmeden hiçbir yerde kullanılmaz.
- **Hekim adı bilinmiyor:** Bölüm "ekip" olarak adlandırılır, ad yazılmaz (Vetripol, PetPlus).
- **Puan değişti:** Puan, yorum sayısı ve tarih notu birlikte güncellenir. Tarih notu olmadan puan gösterilmez.
- **Uzun metin:** Başlıklar `clamp` ile küçülür. PetPlus'taki büyük telefon numarası 759 px altında satır kırar (`15.5vw`).
- **Yavaş bağlantı:** Fontlar `display=swap` ile yüklenir, sistem fontu yedekte. Sayfada fotoğraf yok, ağır görsel yok. Harita yalnızca istenince yüklenir.
- **JS kapalı:** Giriş animasyonu `opacity: 0` ile başladığı için her sayfanın `<head>` kısmında bir `<noscript>` stili var. Bu stil gizli başlayan öğeleri doğrudan görünür yapar. Etkileşimler çalışmaz ama tüm bilgi ve bağlantılar yerinde kalır.
- **WhatsApp hattı yok:** WhatsApp butonu `wa.me` bağlantısıdır. Numara WhatsApp'ta değilse buton "SMS gönder" (`sms:`) olarak değiştirilir.

---

## 2. Klinik klinik

### Vetripol: sakin, sabırlı, anlatan

| Token | Değer | Kullanım |
|---|---|---|
| `--bg` | `#F4EEE3` | Kum rengi zemin |
| `--surface` | `#FBF8F2` | Kartlar |
| `--ink` | `#1E3A31` | Koyu yeşil metin ve puan kartı |
| `--accent` | `#A84A28` | Kiremit: birincil buton, vurgu kelimesi |
| `--clay` / `--clay-2` | `#C4693F` / `#E8B79B` | Kedi çizimi |
| `--soft` / `--soft-2` | `#CBD5C1` / `#E6DCCB` | Acil bölümü zemini, adım kartları |
| `--font-display` | Fraunces (opsz, SOFT ekseni) | Başlıklar, h1'deki italik vurgu |
| `--font-body` | Figtree 400–700 | Gövde |
| `--r-s` / `--r-m` / `--r-l` | 10 / 18 / 28 px | Buton tam yuvarlak (`999px`) |

- **Hero etkileşimi:** SVG kedi. Gözbebekleri (`.pupil[data-cx][data-cy]`) imleci izler, en fazla 11 px yatay kayar. Dikey hareket bunun 0.55 katı. Fare kedinin üstüne gelince, tıklanınca ya da "Kediye yavaşça göz kırp" butonuna basılınca göz kapakları (`.lid`, `scaleY 0 → 1`, 650 ms) kapanıp açılır. İlk seferde altta bir cümle belirir: kediler güvendikleri insana yavaşça göz kırpar. Sayfa açıldıktan 1.5 sn sonra kedi bir kez kendiliğinden göz kırpar.
- **Bölüm anı:** Ulaşım bölümünde dev "Yenişafak" kelimesi, bölüm görününce aşağıdan yükselir (`translateY(105%) → 0`, 900 ms).
- **Özel bileşenler:** "Arayın / Gelin / Plan birlikte" üç adım kartı, "Engelsiz erişim" satırı (Google kaydındaki tekerlekli sandalye, otopark ve tuvalet bilgisi).

### Hiera: modern, titiz, takipçi (Pamukkale travertenleri)

| Token | Değer | Kullanım |
|---|---|---|
| `--bg` | `#F5F3EE` | Traverten beyazı |
| `--ink` | `#0F2429` | Metin |
| `--accent` / `--accent-2` | `#0B6F78` / `#095C63` | Butonlar, acil bölümü zemini |
| `--aqua` / `--aqua-soft` | `#7CCDD1` / `#DCEFEE` | Havuz suyu, hatırlatma notu |
| `--stone` | `#E7E1D4` | Traverten taşları |
| `--font-display` | Instrument Serif (normal ve italik) | Başlıklar |
| `--font-body` | Schibsted Grotesk 400–700 | Gövde, saat tablosu |
| `--r-s` / `--r-m` / `--r-l` | 8 / 14 / 22 px | Butonlar `--r-s` ile köşeli, daha klinik bir his |

- **Hero etkileşimi:** Beş kademeli traverten havuzları (SVG, `g.pool[data-tier][data-x0][data-x1]`). Açılışta havuzlar yukarıdan aşağı dolar (`scaleY 0 → 1`, kademe başına 160 ms gecikme). Fareyle havuzun üstünde gezinince en fazla 260 ms'de bir halka yayılır (`ripple`, 1.1 sn). Tıklayınca o kademeden aşağıya su akar (`flow`, kademe başına 170 ms). "Suyu akıt" butonu aynı akışı klavye ve dokunmatik için tetikler.
- **Özel bileşenler:** 01–04 numaralı hizmet satırları. Saat tablosunda bugünün satırı vurgulanır, ama "şu an açık" ya da "kapalı" yazılmaz. Tablonun altında "Saatler Google kaydından alındı…" notu var.

### Cimihav: mahalle veterineri, sıcak ve esprili

| Token | Değer | Kullanım |
|---|---|---|
| `--mustard` | `#F2B632` | Hero zemini |
| `--paper` | `#FFF8E9` | Sayfa zemini |
| `--sand` | `#F7E4B6` | Hekim bölümü zemini |
| `--ink` | `#231A12` | Metin, kalın kenarlar, kaydırılmış gölgeler |
| `--brick` / `--brick-2` | `#A0381F` / `#86301A` | Birincil buton, acil kutusu |
| Tabela mavisi | `#1F4C9A` | Ulaşım bölümündeki sokak tabelası (sayfa CSS'inde) |
| `--font-display` | Bricolage Grotesque 500–800 | Başlıklar |
| `--font-body` | Instrument Sans 400–700 | Gövde |
| `--r-s` / `--r-m` / `--r-l` | 10 / 14 / 20 px | Kartlarda 2 px mürekkep kenar ve 6 px kaydırılmış gölge |
| `--pop` | `cubic-bezier(.34,1.56,.64,1)` | Zıplayan geçişler |

- **Hero etkileşimi:** Duvarın üstünde köpek ve kedi (`#dog`, `#cat`). Dokununca ya da Enter'a basınca baş zıplar (`hop`, 500 ms) ve "Hav!" ya da "Miyav." balonu açılır (`scale 0 → 1`, 350 ms, `--pop`). Balon 1.8 sn sonra kapanır. Altta "Köpeğe dokunun / Kediye dokunun" butonları da aynı işi yapar. Açılışta ikisi sırayla (1.3 sn ve 2.1 sn) bir kez konuşur.
- **Bölüm anı:** "Selçukbey Mah. / 736 Sk." tabelası, bölüm görününce `rotate(-9deg) → rotate(-1.2deg)` ile yerine oturur.
- **Özel bileşenler:** Koyu "Sokakta yaralı bir can mı buldunuz?" kartı, acil kutusunda sokak hayvanı ipucu.

### PetPlus: düzenli, enerjik, evde de

| Token | Değer | Kullanım |
|---|---|---|
| `--bg` | `#F2F4F7` | Açık gri zemin |
| `--ink` / `--ink-2` | `#0E1A2B` / `#1A2A42` | Lacivert üst çubuk, acil bölümü, kısırlaştırma kartı |
| `--accent` / `--accent-2` / `--accent-hi` | `#C9381F` / `#AE2F19` / `#E2492E` | Birincil buton, artı işareti, koyu zeminde vurgu |
| `--accent-soft` | `#FCE6E0` | Evde veteriner kartı |
| `--font` | Archivo, başlıklarda `font-stretch: 125%` ve 800 | Tek aile, geniş kesimli başlıklar |
| `--r-s` / `--r-m` / `--r-l` | 8 / 16 / 26 px | — |

- **Hero etkileşimi:** "Klinikte / Evde" anahtarı (`#switch`, butonlarda `aria-pressed`, sol ve sağ ok tuşları çalışır). "Evde" seçilince SVG'de klinik tabelası kaybolur, çatı iner, ev ayrıntıları belirir ve artı işareti döner (400–600 ms). Açıklama metni de moda göre değişir.
- **Bölüm anı:** Ulaşım bölümünde dev "0553 800 50 00" numarası. Ortadaki "800" `--accent` renginde. Hover'da rakam grupları sırayla 4 px yükselir (50 ms arayla). Numaranın kendisi arama bağlantısıdır.
- **Özel bileşenler:** Kısırlaştırma zaman çizelgesi kartı (01 tetkik ve kalp değerlendirmesi, 02 operasyon, 03 kontroller).

### Yenişehir Koşuyolu: hızlı, kapsamlı, güven veren

| Token | Değer | Kullanım |
|---|---|---|
| `--teal` / `--teal-2` | `#0B5C63` / `#084A50` | Kliniğin kendi petrol yeşili: hero, üst çubuk, alt bilgi |
| `--teal-soft` | `#DCEDEA` | Simge zeminleri, harita kapağı |
| `--orange` / `--orange-2` | `#F08A24` / `#DB7614` | Kliniğin turuncusu: birincil buton (üstünde koyu metin), liste işaretleri |
| `--cream` / `--sand` | `#FFF6EA` / `#FBEAD3` | Sayfa zemini, acil bölümü zemini |
| `--ink` | `#10282B` | Metin |
| `--font-display` | Red Hat Display 500, 700, 900 | Başlıklar |
| `--font-body` | Red Hat Text 400, 500, 700 | Gövde |
| `--r-s` / `--r-m` / `--r-l` | 10 / 18 / 28 px | Butonlar tam yuvarlak |

- **Hero etkileşimi:** "Şu an acil bir durum mu var?" kartı. Kart açılışta hafif eğik halden yerine oturur (800 ms, 300 ms gecikmeli). "Evet, acil" seçilince turuncu olur ve altında büyük "Şimdi ara" butonu ile üç adım belirir. "Hayır, randevu" seçilince yeşil olur ve WhatsApp randevu butonu çıkar. Cevap alanı 450 ms'de yükselerek gelir (`aria-live="polite"`).
- **Bölüm anı:** Ulaşım bölümündeki dev "Neredeyiz?" kelimesi. Bölüm görününce turuncu soru işareti bir kez sallanır (`wiggle`, 1.2 sn).
- **Özel bileşenler:** Kliniğin Instagram'daki hizmet listesinden dört grup kartı (Muayene ve tanı, Cerrahi, Yatış ve yoğun bakım, Koruyucu ve evde). Ayrıca Instagram, YouTube ve TikTok bağlantıları (Simple Icons, marka renkleri).

---

## 3. Yayına almadan önce

1. `<meta name="robots" content="noindex, nofollow">` ve `.sample-note` şeridini kaldırın.
2. Puan, yorum sayısı ve tarih notunu yayın günü Google Haritalar'dan yeniden okuyun.
3. `data-confirm="hours"` satırlarını klinikten alınan saatlerle değiştirin ve teyit çipini silin.
4. WhatsApp hattını doğrulayın. Hat yoksa butonu `sms:` bağlantısına çevirin.
5. Hekim adlarını klinikle teyit edin (README'deki tabloya bakın).
6. Kliniğin kendi fotoğrafları gelirse çizimlerin yanına ekleyin. Stok ya da üretilmiş fotoğraf kullanmayın.
