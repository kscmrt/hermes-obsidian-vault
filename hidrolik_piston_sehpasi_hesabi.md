# Hidrolik Asansör — Piston Sehpası Boyu Hesabı

**Kaynak belge:** `HİDROLİK ASANSÖR PİSTON SEHPASI BOYU HESABI.pdf`
**Uygulama:** `/home/kscmrt/sonproje` → `/piston-sehpa`
**Dosyalar:** `src/app/piston-sehpa/page.tsx`, `src/components/piston-sehpa/ShaftDiagramSvg.tsx`
**Son commit:** `55db17a` (2026-09-10)

---

## Semboller

| Sembol | Anlam |
|---|---|
| `S` | Piston sehpası boyu |
| `L` | Silindir kapalı boyu |
| `G` | Gerekli strok |
| `K` | Toplam kuyu yüksekliği |
| `x` | Piston açılma miktarı (anlık) |
| `x₀` | **Montaj ön-açılması** |
| `pit` | Kuyu dibi derinliği |
| `over` | Son kat yüksekliği |

## Temel formüller

```
G     = (seyir + kayma_payı) / askı_oranı
h     = G + L + makara_payı
K     = pit + seyir + son_kat
maks_sehpa  = K − h
ideal_sehpa = maks_sehpa − 50
```

**Doğrulanmış örnek (belge, 5/5 birebir):**
pit=1000, seyir=5700, son kat=4000, strok=3800, L=4050, makara=630, kayma=300
→ G=3000, h=7680, K=10700, maks=3020, **ideal=2970 mm**

---

## 7 KURAL

### Kural 1–3 (belgeden)
- **Kural 2:** `piston_stroku ≥ G` (belgede 4 ünlemle)
- **Kural 3:** Tavan boşluğu ≥ 50 mm → `tavan(S) = K − (S + L + G + kasnak)`

### Kural 4 — Halat kolu tükenmesi ⚠️ EN ÇOK YANLIŞ ANLAŞILAN

> **Murat'ın tanımı (verbatim):** *"çarpışma dediği aslında halatı yere paralel olma durumu, kabin seyir mesafesini tamamlamadan halat bitmesine diyoruz"*

**YANLIŞ model:** kasnak ↔ karkas ÜST noktası teması.
Kasnak kabinin **yanındadır** (yan konsol) — karkas kasnağı rahatça geçer, fiziksel temas genelde olmaz.

**DOĞRU model:** kasnaktan karkasın **ALT traversine** inen hareketli halat kolunun tükenmesi.

```
hareketliKol(x) = (S + L + kasnak/2 − kuyuDibi) − x
```

Kol her 1 mm strokta 1 mm kısalır → **en kritik nokta üst kat**.

**Sadeleşmiş sonuç** (ideal sehpa yerine konduğunda S, L, kuyuDibi, seyir sadeleşir):
```
tepedeKalanKol = son_kat − kayma/2 − kasnak/2 − 50
```
→ **Tek belirleyici: SON KAT YÜKSEKLİĞİ.** (pit/seyir/L ne olursa olsun sonuç aynı — 4 senaryoda 3085 mm sabit doğrulandı.)

**Çözüm:** son katı yükselt (1:1 etki). Kasnak çapı / kayma payı **yarı** oranda etki eder.
❌ "Kuyu dibini derinleştir" **yanlıştır** — matematiksel olarak etkisiz.

### Kural 5 — Kuyu dibi iniş payı
Kabin en alt kattayken kabin altı kuyu dibine **≥ 500 mm** inmeli (tampon, karkas altı ekipman, bakım güvenliği).

### Kural 6 — Silindirin ÖN-AÇIK bağlanması ⚠️

> **Murat (verbatim):** *"piston tam kapalı halde halat bağlamak değil, stroğu bir miktar açarak bağlarsa hem kuyu dibine inebilir hem de seyirini tamamlayabilir"*

Montajda piston **kısmen açık** (`x₀`) bağlanır. Tam kapalı bağlanırsa kabin kuyu dibine inemez.

**Türetme:**
```
Kasnak merkezi:  P(x) = S + L + x + kasnak/2
Halat sabit boy: C(x) = 2·P(x) − sabit
Montajda x=x₀ iken kabin alt kat eşiğinde ⇒ C(x₀) = pit

  C(x) = pit + 2·(x − x₀)
```

🔑 **KRİTİK BULGU: bu ifadede S, L ve kasnak SADELEŞİR.**
Kabinin nerede duracağını belirleyen **sehpa boyu değil, montaj ön-açılmasıdır**.
→ Müşterinin elindeki sehpa farklı boyda olsa bile doğru `x₀` ile sistem çalışır.
Doğrulandı: kayma=1000, S=2600/2400/2000/1500 → hepsinde x₀=250, aşağı=500, üst=500.

**x₀ kısıtları:**
```
x₀ ≥ inişPayı / 2                                    (kuyu dibine inebilsin)
x₀ ≤ strok − seyir/2                                 (seyri tamamlayabilsin)
x₀ ≥ şişe + pit + seyir/2 − S − L − kasnak/2         (üst katta şişe payı)
x₀ ≤ K − 50 − S − L − kasnak                         (montajda kasnak tavanı aşmasın)
```

**İdeal:** artık rezerv `2G − seyir = kayma_payı`, iki uca eşit bölünür →
```
x₀ = kayma_payı / 4        (geçerli pencereye clamp edilir)
```

**Kayma payı yeterlilik şartı:** `kayma ≥ 2 × inişPayı` (yani ≥ 1000 mm).
Varsayılan kuyudaki 300 mm **YETMEZ** → pencere 250–150 = geçersiz.

### Kural 7 — Tavana çarpma (kasnak + kabin) ⚠️

En yüksek nokta piston **TAM AÇIKken** (x = G) oluşur. İki cisim **farklı davranır**:

**(a) KASNAK — x₀'dan BAĞIMSIZ**
```
kasnakUstu = S + L + G + kasnak
kasnakUstu + kasnakBosluk <= K
```
İfadede x₀ **YOK**. Kasnak tavana çarpıyorsa **ön-açılma ile ÇÖZÜLEMEZ** —
yalnızca sehpa kısaltılır (veya son kat yükseltilir).
Kural 3'ün sabit 50 mm'si bunun özel hâlidir; artık pay girdiye bağlı.

**(b) KABİN — x₀ için ALT SINIR üretir**
```
kabinUstu(tam acik) = kuyuDibi + 2(G - x0) + karkasYuk
=> x0 >= [kuyuDibi + 2G + karkasYuk + kabinBosluk - K] / 2
```
x₀ büyüdükçe tepe **ALÇALIR** (1 mm x₀ → 2 mm alçalma). Bu alt sınır
`mountPreOpenMin`'e dahildir → Kural 6 penceresini daraltır.

**Doğrulama** (K=7800, G=2500, S=2620, boşluklar 50/50):
| karkas | gereken x₀ | x₀=500'de boşluk | durum |
|---|---|---|---|
| 1800 | 125 | 800 | UYGUN |
| 2200 | 325 | 400 | UYGUN |
| 2600 | 525 | 0 | ÇARPAR |
| 3000 | 725 | −400 | ÇARPAR |

Sınır testi: x₀ = x₀min'de boşluk **tam 50 mm** çıkar → formül doğru.
Kasnak: S 200 mm uzatılınca boşluk −150 → 200 mm kısalt (x₀ etkisiz).

**Karkas yüksekliği girilmediyse kabin satırı "denetlenmedi" der** — uydurma yok.

---

## Halat şişesi (RİJİT eleman — Kural 4'ün eşiği)

Şişe **soyut bir pay DEĞİL, rijit fiziksel tertibattır** — bükülmez, kısalmaz,
boyu kadar yer kaplar (girdi, saha standardı 500 mm).

```
esnek_halat = kol − şişe_boyu
```
Kol şişe boyuna inince **şişe kasnağa DAYANIR** (halat bitmeden önce).
Şişe boyunun her mm'si sehpa penceresinin alt sınırını **1 mm yükseltir**:

| şişe | asgari sehpa | kol=800 iken esnek halat |
|---|---|---|
| 0 | 385 | 800 |
| 300 | 685 | 500 |
| 500 | 885 | 300 |
| 800 | 1185 | **DAYANDI** |

SVG'de kol iki parçalı çizilir: kasnak→şişe üstü **ince esnek halat**,
şişe üstü→kabin altı **dolu rijit gövde** (`SISE nnn`, uyarıda kırmızı).
Eşik sabit değil, girdi. Mevcut sehpa penceresinin **alt sınırını** kaydırır:

| Şişe payı | Asgari sehpa |
|---|---|
| 200 | 85 mm |
| **500** | **385 mm** |
| 800 | 685 mm |

---

## Mevcut (müşterinin kendi) sehpası

**İdeal boy tek nokta değil, bir ARALIĞIN ÜST SINIRIDIR.**

İki kısıt **ters yönlü**:
```
(a) Kural 3 tavan:  S ≤ K − G − L − kasnak − 50     ← ÜST SINIR (= ideal)
(b) Kural 4 kol:    S ≥ şişe + pit + seyir/2 − L − kasnak/2   ← ALT SINIR
```
Uzun sehpa → kasnak tavana çarpar. Kısa sehpa → halat üst kattan önce biter.
Varsayılan kuyuda pencere: **85 – 2970 mm** (şişe 200) / **385 – 2970** (şişe 500).

Panel verir: KULLANILABİLİR / ÇOK UZUN / ÇOK KISA + kaç mm kısalt veya kaç mm takoz.

---

## 2:1 palanga kinematiği

Piston 1 mm açılır → kasnak 1 mm yükselir → sol kol 1 mm uzar → toplam boy sabit olduğundan sağ kol 1 mm kısalır → kasnak 1 + kol 1 = **kabin 2 mm**.

- Halat **underslung**: karkasın **ALT** traversine bağlanır (üstte değil).
- Rota: kuyu dibi sabit ucu ↑ kasnak ↓ karkas alt traversi.
- Simülasyonda toplam halat boyu her konumda **sabit** olmalı (varsayılan kuyuda 17.370 mm, sapma 0,0 mm).
- ⚠️ Kayma payı simülasyona **girmez** — uç rezervidir. Piston açılması `kabin_hareketi / 2`.

---

## Simülasyon (ShaftDiagramSvg.tsx)

**Piston x₀ ofsetli çizilir:**
```
currentStrokeMM = preOpenMM + currentTravelMM / susRatio
```
Krom milin ön-açık bölümü amber bantla + `MONTAJ x₀` etiketiyle gösterilir (kalıcı referans).

**Simülasyon tüm strok aralığını gezer (kat eşikleriyle sınırlı DEĞİL):**
```
simMin = −(2·x₀) / seyir                        → piston 0 (tam kapalı), kuyu dibi
simMax = 1 + (2(G−x₀) − seyir) / seyir          → piston G (tam açık)
simPosition ∈ [simMin, simMax];  0 = alt kat eşiği, 1 = üst kat eşiği
```
Toplam kabin hareketi = **2G**. x₀ = kayma/4 olduğunda alt ve üst rezerv **simetrik**.
Butonlar: KUYU DİBİ / ALT KAT / ORTA / ÜST KAT / TAM AÇIK (uçlar amber = seyir dışı rezerv).

⚠️ Sık hata: sadece alt sınırı açıp üst sınırı `1`de bırakmak — üst kata varıldığında piston hâlâ `G − x₀ − seyir/2` kadar rezerv taşır.

⚠️ **TDZ tuzağı:** `simMinRef`/`simMaxRef`'i senkronize eden `useEffect`'ler, `simMin`/`simMax` tanımından **SONRA** konmalı; önce yazılırsa `ReferenceError: cannot access before initialization`.

---

## PDF çıktıları (2 ayrı buton)

| Buton | Fonksiyon | İçerik |
|---|---|---|
| Çizim Sayfası (1 Sayfa) | `handleDownloadPdf` / `pdfRef` | Eski tek sayfalık teknik şema |
| Teknik Rapor (3 Sayfa) | `handleDownloadReport` / `reportRef` | S1 kapak+simülasyon ilk hali, S2 7 kural denetimi, S3 türetmeler |

`handleDownloadReport` → `reportRef` içindeki her `[data-a4]` düğümü ayrı A4 sayfası
(`toJpeg` + `pdf.addPage()` döngüsü). **Sayfa eklemek için sadece yeni `<div data-a4>` yazmak yeterli.**

Rapor `simPosition={0}` (alt kat eşiği) basar — tekrarlanabilir belge için,
kaydırıcının anlık konumunu değil.

---

## Tuzaklar

- `carTopHeight` girdisi **hesaba girmez**, sadece şemayı ölçekli çizer.
- Silindir tipi **tek kademe sabit** (select yok).
- PDF önizlemesi `scale-[0.42]` → içine simülasyon koyma, okunmaz. PDF'te statik (`isPdf=true`), ekranda tam boy panel (560×860).
- Chunk doğrulamasında `grep` Türkçe metni bulamaz (JS `\uXXXX`) → `python3 codecs.decode(raw,'unicode_escape',errors='ignore')`.
- PDF adı Türkçe karakterli → `read_file` bozulur, `glob('*SEHPASI*.pdf')` + `fitz` kullan.

- ⚠️ **PDF önizlemeyi gizlerken `display:none` / `opacity:0` KULLANMA.**
  `html-to-image` (`toJpeg`) yalnızca gerçekten render edilmiş düğümü görüntüler;
  gizlenirse PDF **boş/siyah** çıkar. Doğrusu: DOM'da tut, `fixed -left-[9999px]`
  ile ekran dışına taşı.
- ⚠️ Değişken adları: `ropeLegAtTop` (nullable!), `mountDescentOk`, `valPistonStroke`,
  `strokeEntered`. Rapor yazarken `rule4LegAtTop` / `pitDescentOk` / `valStroke`
  diye uydurma isimler build'i kırar.

---

## Girdi politikası (2026-09-10)

- **Kayma payı: VARSAYILAN YOK** (`useState('')`). "300 mm önerilir" metni silindi —
  proje değeri uydurulmaz. Girilmediyse amber uyarı: *"Kayma payı girilmedi —
  Kural 6 denetlenemiyor."* (`slipEntered` bayrağı). kayma=0 → x₀=0, iniş=0,
  Kural 6 anlamsız; sessizce 0 göstermek yerine açıkça söylenir.
- **Kat eşiği = KABİN TABANI** (kabin altına sabit). Kabin alt kattayken *tabanı*
  tam o kotta durur; yolcu eşikten düz basar. Karkas alt traversi ve halat şişesi
  bu kotun ALTINDA kalır — onlar eşik referansı **değildir**.
- Denetlenemeyen kural "DENETLENMEDİ" der (Kural 2 strok, Kural 7 karkas, Kural 6 kayma).

---

## Kabin modeli (2026-09-10 düzeltmesi)

**Kavram karışıklığıydı:** SVG kabini SABİT 2200 mm çiziyordu, `carTopHeight`
girdisi ise "karkas üst KOTU" (kuyu dibinden mutlak) sayılıyordu → kabin girdiye
tepki vermiyordu, üstelik Kural 7 ile SVG farklı karkas kotu kullanıyordu.

**Doğrusu:** kabin sabit boyutlu bir KUTUDUR, kuyu içinde yalnızca ÖTELENİR.
```
cabinH_MM   = carTopHeight            (girdi: KABİN YÜKSEKLİĞİ)
traversPayı = max(80, kabinYük·0.06)
karkasÜst   = kuyuDibi + hareket + kabinYük + traversPayı
```
Aynı `slingTopPad` page.tsx'te de var → Kural 7 ile SVG **aynı kotu** kullanır.

| kabin | karkas üst | tepede boşluk | durum |
|---|---|---|---|
| 1800 | 1908 | 692 | UYGUN |
| 2200 | 2332 | 268 | UYGUN |
| 2600 | 2756 | −156 | ÇARPAR (x₀≥603) |
| 3000 | 3180 | −580 | ÇARPAR (x₀≥815) |

## Dikey kaydırıcı

Şema 560 px; sağındaki boşluğa dikey kumanda kolonu konuldu.
```
writing-mode: vertical-lr;  direction: rtl;
```
⚠️ **`direction: rtl` ŞART** — olmazsa kaydırıcı TERS çalışır (yukarı sürükleyince
kabin aşağı iner). Bu haliyle üst = tepe, alt = kuyu dibi.
Mobilde dikey kolon gizli, yatay kaydırıcı görünür (`lg:hidden` ile çift kontrol yok).

---

## Sayfa yerlesimi (2026-09-10, `82a902c`)

**Tespit:** sol kolon 4/12 genislikte ama 339 satirlik kural panelini tasiyordu;
sagdaki simulasyon bitince buyuk bos alan kaliyordu. Dar yerde cok icerik,
genis yerde hic icerik.

| Degisiklik | Deger |
|---|---|
| Kurallar | sol -> sag kolon, `xl:columns-2` + `break-inside-avoid` |
| Kolon orani | 4/8 -> **3/9** |
| Girdi kolonu | `lg:sticky lg:top-4` + kendi icinde kaydirilir |
| Ozet seridi | en ustte 7 kutucuk + "N KURAL SAGLANMIYOR" rozeti |

Panel yukseklikleri degisken oldugu icin **grid degil `columns`** kullanildi
(grid bosluk birakirdi).

### Tuzak: sticky + stretch
`grid`'e **`items-start` eklenmeli**. Varsayilan `align-items: stretch` sticky'yi
SESSIZCE etkisiz birakir (element zaten tam yukseklikte olur, yapisacak yer yok).

### Ozet seridi kurali
Serit **YENI hesap yapmaz** — panellerin kullandigi ayni bayraklari okur:
`feasible, strokeOk, standWindowValid, rule4Ok, mountDescentOk, mountOk, ceilingOk`.
Boylece serit ile panel birbirinden sapamaz. Girdi yoksa `null` -> gri tire
"denetlenmedi" (uydurma yesil yok).

### HATA: sahte-yesil (bu turda bulundu ve duzeltildi)
Serit ilk halinde Kural 3 icin `clearanceTopAtIdeal >= requiredStroke + 50`
yaziyordu. Ama `clearanceTopAtIdeal` ZATEN `requiredStroke + 50` olarak tanimli
-> karsilastirma **her zaman true**, kural asla kirmiziya donemezdi.
Gercek denetim `standWindowValid` (`standWindowMin <= standWindowMax`) ile
degistirildi, etiket "Sehpa Penceresi" yapildi.
**Ders:** bir bayragi serit/ozet icin yeniden yazma; mevcut panel bayragini bagla.

## Kompakt yerlesim (`55db17a`)

| Bolge | Once | Sonra |
|---|---|---|
| Girdiler | `grid-cols-2` (4 adet) | tek satir: etiket `basis-[52%]` sol, alan `grow h-8` sag |
| PDF butonlari | sag kolon, genis `px-6 py-2` | sol kolon en ust, `h-8 text-[11px]`: "Cizim (1s)" / "Rapor (3s)" |
| Kabin konumu | semanin ALTINDA | simulasyonun EN USTUNDE |
| Sema | `w-full h-auto` | + `max-h-[calc(100vh-13rem)]` |

### Tuzak: SVG `h-auto` viewport tasmasi
`w-full h-auto` yukseklige SINIR koymaz -- yukseklik genislikle orantili buyur,
uzun kuyularda ekrani tasar. Cozum `max-h-[calc(100vh-13rem)]` (viewBox orani korunur).

**KRITIK:** bu sinir `isPdf` iken UYGULANMAMALI:
```
${isPdf ? "" : "max-h-[calc(100vh-13rem)]"}
```
Aksi halde A4 ciktisi kirpilir. Ekran kisiti rapora sizmamali.

Ayrica SVG sarmalayicisi `shrink-0` -> `shrink min-w-0` (dar ekranda daralabilsin),
dikey kaydirici `minHeight:420px` -> `height:100% + minHeight:260px`.


## Kritik sunucu tuzagi (525d0c0)
- `.next/standalone` build sirasinda silinip yeniden yaratilirsa, calisan node sureci eski silinmis inode'a bagli kalir -> `.next/static` hic kopyalanmamis olur -> SITE GENELINDE tum JS/CSS chunk'lari 500 doner (tek sayfa degil). Belirti: HTML 200 ama chunk 500, sayfa bos/spinner gorunur. Fix: `fuser -k 3000/tcp` ile eski sureci oldur, `npm run start:standalone` ile yeniden baslat (statik kopyalama script icinde).
- Kural paneli tasarim ilkesi: girdi satirlarinda Label+Input ayni `flex items-center gap-2` satirinda, ama ACIKLAMA `<p>` o satirin ICINE degil, DISINA (alt satira) konmali - aksi halde uzun aciklama metinleri sag/alt kenardan kirpilir. 8 girdi satirinda bu hata tekrarlanmisti, tek pattern ile toplu duzeltildi.
- Kural 6 (on-acik montaj) kayma payi bosken x0=0 varsayimiyla kesin 'UYGUN DEGIL' basiyordu - artik slipEntered=false iken 'DENETLENMEDI' gosteriliyor. Ozet seridi 'Kuyu Dibi' onceden yanlis bayraga (mountDescentOk) bagliydi, dogru bayrak pitClearanceOk'a baglandi.
- Dogrulama yontemi: AuthProvider giris duvari puppeteer'i engelliyordu; kullanicidan test giris bilgisi istenip alindi, puppeteer+gercek oturum ile DOM olculdu, vision_analyze ile ekran goruntusu (kirpilmis PNG parcalari halinde, tam boy timeout veriyor) teyit edildi.

## PDF Teknik Rapor Incelemesi (b05cf70)
Kullanicinin paylastigi ureilmis PDF raporda 3 sorun bulundu, canli sayfa (525d0c0) ile
senkron olmadigi tespit edildi:
- Kural 5 rozeti raporda yanlis bayrak (mountDescentOk yerine pitClearanceOk olmali) kullaniyordu.
- Kural 6, kayma payi bos oldugunda (valSlip=0 varsayimiyla) kesin x0 sonucu basiyordu; simdi
  canli sayfadaki gibi "DENETLENMEDI" gosteriyor.
- Ozet tabloda "Kayma payi: 0 mm" yaniltici degeri yerine "girilmedi" yaziyor.
Ders: canli sayfa (/piston-sehpa formu) ve PDF rapor (data-a4 bloklari) AYRI kod bloklarinda
render ediliyor -> bir tarafa yapilan mantik duzeltmesi otomatik digerine yansimiyor,
her ikisi de manuel senkron edilmeli. Son commit: b05cf70.
Git push tamam.

## Kasnak-Tavan Girdisi Kural 3/4'e Baglandi (c2b24ad)
Kullanici sordu: "kasnak tavan mesafesini hic bir hesapta kullanmiyorsun,
ikinci gorselde sabit almissin". Dogru tespitti. Kural 3'un ideal sehpa boyu
formulunde (S = K - h - 50) ve turevlerinde (Kural 4 tepedeKol, mevcut sehpa
denetimi, montaj tavan kontrolu, 300cm son kat senaryosu, PDF rapor
formulleri) belge sabiti 50mm hardcode'lanmisti; "Kasnak-Tavan (mm)" girdisi
(varsayilan 50, ayni deger) SADECE Kural 7'de (piston acikken tepe kontrolu)
kullaniliyordu. Kullanici bu girdiyi degistirdiginde ideal boy hic
etkilenmiyordu -- kullanici karar: "sabit 50mm SILINSIN, benim girdigim
deger kullanilsin".
Fix: 7 hesap noktasi (idealStandHeight, clearanceTopAtIdeal, ropeLegAtTop,
rule4RightSide, actualTopOk, mountCeilingOk, cappedIdeal) + goruntu
metinleri + PDF rapor formulleri valPulleyCeilGap'e baglandi.
Puppeteer canli dogrulama: Kasnak-Tavan 50->100mm -> ideal boy 3120->3070mm
(tam -50 fark, dogru). Son commit: c2b24ad. Git push tamam.

DERS: kullanicinin "bu deger hic kullanilmiyor" tespitleri genelde dogru
cikiyor -- kod okumadan varsayim yapmadan once mutlaka grep ile TUM
kullanim noktalarini (7+ yer olabiliyor) taramak gerekiyor, tek nokta
duzeltip birakmak yetersiz kaliyor.
