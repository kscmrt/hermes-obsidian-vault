# 🌌 Kanal 5: 16:9 Uzun Belgesel & Dark Science Pipeline (@MysteryAuditGlobal)

## 🎯 Konsept & Format
- **Kanal:** Mystery Audit Global (`@MysteryAuditGlobal`)
- **Format:** 16:9 Yatay (1920x1080 Full HD), 30 FPS.
- **Süre:** 5 - 15 Dakika (Minimum 5 dakika / 10 Bölümlü Master Dossier).
- **Görsel Dil:** 2.5D Ken-Burns arşiv pan/zoom, CRT tarama çizgileri, Gizliliği Kaldırılmış (Declassified) CIA/Devlet damgaları, istatistik kartları ve dinamik altyazı.
- **Seslendirme:** Derin karanlık belgesel spikeri (`en-US-ChristopherNeural` / Google Gemini Flash Voice `Charon`).
- **Müzik:** Düşük seviyeli gerilim ve gizem atmosfer müziği (Ducking ile %6 volume).

---

## 🏗️ Üretim ve Render Mimarisi

### 1. Dosya Konumları
- **Kompozisyon:** `/home/kscmrt/remotion-video/src/LandscapeDocu/index.tsx`
- **Props Şablonu:** `/home/kscmrt/remotion-video/public/props_mkultra_master.json`
- **Üretim Motoru:** `/home/kscmrt/remotion-video/render_long_docu_chunks.py`
- **Çıktı Dizini:** `/data/video_outputs/channel5-dark-science/long_form/`

### 2. Parçalı (Chunked) Hızlı Render
Uzun videolar (5+ dk / 9.000+ kare) sunucu zaman aşımlarını engellemek için bölüm bazlı renderlanır ve ffmpeg ile kayıpsız birleştirilir:
```bash
python3 /home/kscmrt/remotion-video/render_long_docu_chunks.py
```

### 3. SEO ve Yayın Paketi
Her uzun belgesel için otomatik oluşturulan dosyalar:
- `thumbnail.jpg` (1920x1080 Yüksek Kontrastlı Kapak)
- `metadata.json` (3 Alternatif Başlık, Zaman Damgalı Açıklama, Etiketler, Sabit Yorum)
- `Project_MKUltra_Full_Documentary_1080p.mp4` (Bitmiş Master Video)
