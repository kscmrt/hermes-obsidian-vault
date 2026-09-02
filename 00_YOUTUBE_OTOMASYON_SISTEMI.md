## 🚀 7/24 Otonom Üretim Servisi (PM2)
Sistem tamamen sıfır maliyetli ve otonom olarak arka planda çalışmaktadır.
- **Master Script**: `/home/kscmrt/remotion-video/autopilot_master.js`
- **PM2 Süreç Adı**: `shorts-autopilot`
- **Yayın Saatleri**: Günde 3 video (09:00, 13:00, 18:30)
- **Özellikler**:
  1. Çoklu RSS (TRT, NTV, AA vb.) + `seen_news.json` ile mükerrer haber engelleme.
  2. Viral 4 aşamalı senaryo + Pinned Comment (Sabit yorum) üretimi.
  3. Pexels API ile sahneye özel dikey HD MP4 B-Roll indirme.
  4. Edge-TTS Türkçe Spiker + Ses kurgusu (Müzik ducking + SFX).
  5. Remotion Full HD 1080x1920 dikey render (Hormozi karaoke altyazı, cam bilgi kartları).
  6. Otomatik disk temizliği (Eski geçici dosyaların ve eski renderların silinmesi).

---

# YouTube Otomasyon Sistemi

Bu dosya Hermes'in kalici hafizasinin (Obsidian Vault) ilk dosyasidir.

## Mevcut Altyapi
- Video uretim kodlari /home/kscmrt/remotion-video/ klasorunun icindedir.
- 2. Kanal uretim (evergreen) islemleri genellikle /home/kscmrt/remotion-video/autopilot/ klasorundeki autopilot_runner.js scripti ile tetiklenir.
- Yeni komutlar veya surecler ogrendikce, bu klasore yeni .md dosyalari ekleyerek veya bu dosyayi guncelleyerek hafizani taze tut.
