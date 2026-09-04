# 🤖 Hermes Autonomous Dev & Healer Multi-Agent Mimarisi

- **Tarih:** 2026-09-04
- **Konum:** `/home/kscmrt/remotion-video/hermes_autonomous_dev_agent.js` ve `/home/kscmrt/remotion-video/hermes_autonomous_healer.js`
- **PM2 Servisleri:** `hermes-healer-bot` (Operasyonel Slot & Süreç Kurtarma) & `hermes-dev-agent` (AI Hata Analiz & Kod Onarım Ajanı)

---

## 🎯 2 Kademeli Otonom Ajan Mimarisi

### 1. Kademe: `hermes-healer-bot` (Operasyonel Kurtarma)
* 8 kanalın günlük yayın planını (`MASTER_SCHEDULE`) 3 dakikada bir tarar.
* Render veya crash sebebiyle kaçırılan slotları tespit eder ve kanal üretim motorunu tetikleyerek eksik videoyu tamamlar.
* Kilitlenen `queue.json` görevlerini (`processing` -> `pending`) sıfırlar ve `/home/kscmrt/tmp` disk temizliğini yapar.

### 2. Kademe: `hermes-dev-agent` (Yapay Zeka Hata Teşhis & Kod Onarım Ajanı)
* PM2 çökme ve hata loglarını 2 dakikada bir analiz eder.
* `ReferenceError`, `SyntaxError`, `TypeError` veya Remotion render çökmelerinde:
  1. Hata veren dosya ve satır numarasını tespit eder.
  2. Gemini 2.5 Flash ile kök neden analizi yapar.
  3. Güvenli yedek (`.bak`) alarak kod dosyasını otomatik olarak yamalar.
  4. `node -c` ile syntax doğrulaması yapar; geçerse PM2 servisini yeniden başlatır, geçmezse geri alır.
  5. Tüm onarım sürecini `Agent_Bug_Fix_Logs.md` dosyasına kaydeder.
