# YouTube Shorts 3 Kanallı Otonom Üretim Sistemi (Isolated 7/24)

Bu sistem, 3 farklı nişteki YouTube kanalını birbirinden tamamen bağımsız ve izole olarak 7/24 yöneten otonom Remotion render ve yayın mimarisidir.

---

## 📺 Kanal Mimarisi ve İzolasyon

| Kanal | Konsept & Niş | Dizin | PM2 Süreci | Spiker | Günlük Yayın Saatleri |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **1. Kanal** | **Gündem & Son Dakika Haber** | `/home/kscmrt/remotion-video/channels/channel1-haber/` | `channel1-haber` | `tr-TR-AhmetNeural` | 09:00, 13:00, 18:30 |
| **2. Kanal** | **Beyaz Eşya & Kombi Arıza Rehberi** | `/home/kscmrt/remotion-video/channels/channel2-ariza/` | `channel2-ariza` | `tr-TR-EmelNeural` | 10:30, 15:30 |
| **3. Kanal** | **Otomobil Arıza & Gösterge İkazları** | `/home/kscmrt/remotion-video/channels/channel3-oto/` | `channel3-oto` | `tr-TR-AhmetNeural` | 11:30, 17:00, 20:30 |

---

## 🛠️ Her Kanalın İzole Yapısı
Her kanal klasörü kendi bağımsız bileşenlerine sahiptir:
- `engine.js` : Otonom döngü, RSS/Kuyruk yönetimi, Pexels B-roll indirme, TTS ve Remotion render tetikleyici.
- `queue.json` / `seen_news.json` : Kanala özel mükerrer kontrolü ve içerik kuyruğu.
- `output/` : Kanala ait üretilmiş MP4 videolar ve props kayıtları.
- `token.json` : Kanala özel bağımsız YouTube OAuth yetkilendirmesi.

---

## ⚡ Video Tasarım & Kalite Standartları
- **Dikey Format**: 1080x1920 (9:16) Full HD, 30 FPS.
- **Dinamik B-Roll**: Konuya uygun hareketli Pexels MP4 video katmanları.
- **Hormozi Karaoke Altyazı**: Kelime bazlı, sarı/yeşil vurgulu modern altyazı animasyonu.
- **Görsel Katmanlar**: TV yayın standardında canlı başlık bantları, dinamik istatistik kartları ve sayaçlar.
- **Ses Tasarımı**: Doğal Edge-TTS yapay zeka spikeri, arka plan tematik müziği (audio ducking ile kısık seviye) ve Whoosh geçiş efektleri.

---

## 🌐 Web Yönetim Kontrol Paneli (Dashboard)

Tüm kanalları tek bir ekrandan canlı izlemek, manuel video tetiklemek, kuyruk yönetmek ve üretilen videoları tarayıcıdan izlemek için merkezi web arayüzü yayındadır:
- **Yerel Ağ**: `http://192.168.1.160:8080`
- **Tailscale / Uzak Erişim**: `http://100.81.238.46:8080`
- **PM2 Süreç Adı**: `shorts-dashboard` (Port: 8080)

### Panel Yetenekleri
1. **Canlı İzleme**: 3 kanalın CPU, RAM, Uptime ve render durumları gerçek zamanlı izlenir.
2. **Tek Tıkla Üret**: "Şimdi Üret" butonuyla anında video render döngüsü başlatılabilir.
3. **Kuyruk Yönetimi**: 2. ve 3. kanallar için doğrudan arayüzden yeni arıza kodu/içerik eklenebilir.
4. **Dahili Video Player**: Üretilen 1080x1920 dikey Shorts videoları tarayıcıdan sesli oynatılabilir ve indirilebilir.
5. **Canlı Loglar**: Her kanalın konsol çıktıları popup terminal ekranında canlı akar.

---

## 🚀 Yönetim ve Kontrol Komutları

```bash
# Tüm botların durumunu inceleme
pm2 list

# Belirli bir kanalın canlı loglarını izleme
pm2 logs channel1-haber
pm2 logs channel2-ariza
pm2 logs channel3-oto

# Tek seferlik manuel tetikleme
node /home/kscmrt/remotion-video/channels/channel1-haber/engine.js
node /home/kscmrt/remotion-video/channels/channel2-ariza/engine.js
node /home/kscmrt/remotion-video/channels/channel3-oto/engine.js
```
