# 🎬 Türkiye Simülasyonu (2D Animasyon & Belgesel Dizi Motoru)

**Tarih:** 2026-09-02  
**Konsept:** Günümüz Türkiye'sinde yaşayan, ekonomik ve sosyal zorluklarla mücadele eden, bıkmış/tükenmiş bir Türk gencinin ("Emre") hayatını mizahi-belgesel (sitcom/satir) formatında anlatan özgün 2D çizgi animasyon serisi.  
**Format:** 9:16 Shorts / Reels / TikTok ve 16:9 Uzun YouTube Belgesel Serisi  
**Maliyet:** 0 TL (Yerel render + Edge-TTS + Procedural 2D Rigging)

---

## 🎨 Karakter ve Sahne Anatomisi (Emre)
- **Görsel Tasarım:** Kurzgesagt / Casually Explained / OverSimplified temiz vektör estetiği.
- **Yüz & Mimikler:**
  - Göz altı morlukları / torbaları (tükenmişlik hissiyatı).
  - Canlı göz kırpma (blinking) ve etrafa kayan göz bebekleri.
  - Alaycı / yorgun kaş hareketleri.
  - Sese duyarlı otomatik ağız açıp kapama (lip-sync).
- **Fizik:** Sürekli ince nefes alma / omuz yaylanması (`math.sin(frame)` fizik döngüsü).
- **Dekor / Çevre:**
  - Gece yağmurlu şehir manzaralı pencere.
  - Duvarda eğri asılı "Üstün Başarı" diploması.
  - Masada dumanı tüten ince belli çay bardağı ve iş başvuruları açık laptop.

---

## 🚀 Üretim Dosyaları & Konumlar
- **Render Scripti:** `/home/kscmrt/remotion-video/render_emre_pilot.py`
- **Pilot Video Çıktısı:** `/home/kscmrt/remotion-video/output/turkiye_simulasyonu_pilot.mp4`
- **Önizleme Karesi:** `/home/kscmrt/remotion-video/output/pilot_preview.png`
- **Ses Dosyası:** `/home/kscmrt/remotion-video/public/emre_voice.mp3`

---

## 📺 Bölüm Senaryo Formatı
Her bölüm 3 temel sahneden ve vurucu bir sondan oluşur:
1. **Giriş / Durum Tespiti (0-6s):** Absürt bir sabah veya günlük rutin anı (ör. çalar saat, faturaya bakış).
2. **Kıyaslama / Gerçekler (6-15s):** İnfografik kartlarla trajikomik gerçekler (CV başvuruları, kira/maaş oranı, kahvaltı maliyeti).
3. **Kapanış / Vurgu (15-22s):** *"Hoş geldiniz, burası Türkiye Simülasyonu"* damgası ve abone ol çağrısı.
