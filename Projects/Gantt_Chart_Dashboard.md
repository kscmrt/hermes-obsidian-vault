# Dashboard & Gantt Chart Mimarisi (2026 Güncel)

## 1. Dashboard Genel Bakış (Port 8080)
- **Tema**: Profesyonel Light Mode (#f8fafc / #ffffff / #0f172a).
- **Gantt Çizelgesi Sekmesi (`/api/gantt`)**:
  1. **Haftalık 16:9 Uzun Belgesel & Masterclass Gantt Şeması**:
     - 7 Günlük takvimde 9 kanalın haftalık uzun video üretim ve yayın durumu.
     - Durumlar: `Tamamlandı` (Yeşil), `Bugün Yayında / İşleniyor` (Mavi/Animasyonlu), `Planlandı` (Gri).
  2. **24 Saatlik Günlük Shorts Akış Çizelgesi**:
     - 9 kanalın gün içerisindeki tüm slot saatleri ve otonom render durumları.
  3. **Güvenlik & Metrikler**:
     - Mutex Lock koruması aktif.
     - EBU R128 (-14 LUFS) mastering standardı.
     - Otonom Healer & Dev Agent aktif.
