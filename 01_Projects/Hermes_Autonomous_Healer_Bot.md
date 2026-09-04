# 🛡️ Hermes Autonomous Channel Healer & Watchdog Bot

- **Tarih:** 2026-09-04
- **Konum:** `/home/kscmrt/remotion-video/hermes_autonomous_healer.js`
- **PM2 Servis Adı:** `hermes-healer-bot`
- **Periyot:** 7/24 kesintisiz (3 dakikada bir tam sağlık ve hata düzeltme taraması)

---

## 🎯 Botun Görevleri ve Otonom İyileştirme Mekanizması

1. **Kaçırılan Slotları Otomatik Üretme (Missed Slot Auto-Recovery):**
   - 8 kanalın tüm günlük yayın planını (`MASTER_SCHEDULE`) tarar.
   - Zamanı geçmiş (> 20 dk) fakat diskte veya YouTube'da videosu bulunmayan slotları anında tespit eder ve ilgili kanal motorunu otonom tetikleyerek videoyu üretir ve yayına sokar.
2. **PM2 Servis İyileştirme (Process Crash Healer):**
   - Çöken veya duran (`errored`, `stopped`) kanal daemon'larını otomatik yeniden başlatır.
3. **Kilitlenmiş Kuyrukları Kurtarma (Stuck Queue Recovery):**
   - `queue.json` dosyalarında 30 dakikadan uzun süre `processing` durumunda asılı kalan görevleri `pending` durumuna sıfırlar.
4. **Disk & Bozuk Dosya Temizliği (Auto Purge):**
   - 0-byte veya bozuk `.mp4` video artıklarını ve `/home/kscmrt/tmp` altındaki eski Chromium geçici dosyalarını temizler.
5. **Canlı Durum ve Loglama:**
   - Metrikleri `/home/kscmrt/remotion-video/data/pipeline_health_status.json` dosyasına işler ve Dashboard (:8080) ile senkronize tutar.
