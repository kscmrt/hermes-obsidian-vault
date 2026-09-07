# 🎨 Hibrit Sıfır Maliyetli AI Görsel & B-Roll Motoru (9 Kanal + 16:9 Belgesel)

*Tarih: 2026-09-07*  
*Konum: `/home/kscmrt/remotion-video/shared/media_fetcher.js`*

---

## 🚀 Genel Bakış
YouTube videolarında Pexels ve Pixabay stok sitelerinin yetersiz kaldığı, tekrara düştüğü veya konuyla alakasız kaldığı durumları çözmek için **$0 maliyetli Generative AI Görsel Motoru (Pollinations.ai Flux / SDXL)** tüm kanallara entegre edilmiştir.

---

## 🎯 9 Kanal İçin Tanımlı Master Görsel Dili (Aesthetic Style Anchors)

1. **Haber & Gündem (@cahitx):**
   * *Stil:* Journalistic photojournalism, breaking news press coverage, official press room, authentic broadcast visual, professional cinematography, 8k.
2. **Hata Kodu & Ev Aletleri (@hatakodu):**
   * *Stil:* Heating boiler technical maintenance, appliance repair, boiler internal circuit, pressure gauge manometer, 3D technical illustration exploded view, 8k.
3. **Oto & OBD2 Mekanik (@otokod):**
   * *Stil:* Modern car engine bay compartment closeup, automotive mechanic garage workshop, OBD2 diagnostic scanner computer, catalytic converter exhaust system, 8k.
4. **Tüketici Hakları & Hukuk (@hakkinibil):**
   * *Stil:* Legal justice courtroom with scales of justice and gavel, official consumer rights contract signing, modern smartphone refund receipt, 8k.
5. **Dark Science & Mystery (@MysteryAuditGlobal):**
   * *Stil:* 1970s-1990s declassified archival dossier, vintage analog photography, dimly lit secret investigation desk, red evidence thread, top secret stamp, 8k.
6. **Dua Penceresi (@duapenceresi):**
   * *Stil:* Serene grand mosque arched corridor, soft morning golden sunbeams through ornate stained glass, Holy Quran on carved wooden rehal stand, 8k.
7. **Kadim Kıssalar (@kadimkissalar):**
   * *Stil:* Ancient historical Middle Eastern caravan oasis at golden hour, wise elderly sage with white beard in traditional robes, rich oil painting realism, 8k.
8. **Global Quran & Peace (@peacefulduais):**
   * *Stil:* Peaceful majestic misty mountain landscape at sunrise, calm flowing river and divine golden light rays, serene meditation atmosphere, 8k.
9. **Mistik Fısıltı (@mistikfisilti):**
   * *Stil:* Celestial astrology tarot cards, glowing golden constellations, deep cosmos nebula purple and gold dust, mystic candle flame, 8k.
10. **16:9 Uzun Belgesel & Masterclass:**
    * *Stil:* Cinematic 16:9 documentary frame, masterclass visual storytelling, wide angle, hyper-realistic photography, volumetric lighting, 8k.

---

## ⚡ Katmanlı Medya Arama & Hata Önleme Hiyerarşisi

1. **Maneviyat / Hikaye / Gizem Kanalları (CH5, CH6, CH7, CH8, CH9, Belgesel):**
   * **1. Öncelik:** Sahneye özel üretilen $0 AI Görseli (Pollinations Flux - 1080x1920 / 1920x1080)
   * **2. Öncelik:** Pexels Video / Pixabay Video
   * **3. Öncelik:** Pixabay / Pexels Yüksek Çözünürlüklü Fotoğraf
   * **4. Öncelik:** Yerel Garantili Fallback

2. **Haber / Teknik / Hukuk Kanalları (CH1, CH2, CH3, CH4):**
   * **1. Öncelik:** Pexels Video / Pixabay Video (Hareketli gerçek görüntü)
   * **2. Öncelik:** Sahneye özel teknik AI Görseli (Şema, arıza parçası, mahkeme salonu vb.)
   * **3. Öncelik:** Stok Fotoğraf
   * **4. Öncelik:** Yerel Garantili Fallback

---

## 🎬 Remotion Ken Burns & Dinamik Animasyon
Tüm Remotion şablonları (`ApplianceFix`, `CarWarning`, `DynamicNews`, `KissalarShorts`, `DuaShorts`, `GlobalDuaShorts`, `LandscapeDocu`) statik görselleri algılayıp `%100 -> %118` aralığında dinamik kamera yaklaşması (zoom), hafif yatay/dikey kaydırma (pan) ve sinematik vinyet gölgelendirmesiyle tam video hissiyatında render eder.
