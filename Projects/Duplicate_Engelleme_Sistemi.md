# Video Tekrarı (Duplicate) Engelleme Mimarisi

Tüm kanallarda videoların tekrara düşmesini %100 engelleyen çok katmanlı koruma sistemi devreye alınmıştır.

## Koruma Katmanları:
1. **Veritabanı Geçmişi (`shared/dedup_manager.js`):**
   - Her kanalın altında `db/seen_history.json` tutulur.
   - Yüklenen her videonun kimlik kodu (`P0171`, `ECA_40`, `UCAK_600`), başlığı ve YouTube linki kalıcı olarak kaydedilir.
2. **Kuyruk Öncesi Çift Kontrol:**
   - Render başlamadan önce `isDuplicate(channelDir, id, title)` fonksiyonu geçmişi tarar.
   - Daha önce üretilmiş veya yüklenmiş hiçbir konu tekrar seçilmez.
3. **Kuyruk Bittiğinde Güvenli Duruş:**
   - Kuyruktaki tüm konular tükendiğinde motor baştaki videoları tekrarlamak yerine güvenli duruşa geçer ve konsola uyarı bırakır.
4. **Haber Kanalı (`seen_news.json`):**
   - RSS'ten gelen haberler başlık ve kaynak link hash'ine göre karşılaştırılır; daha önce işlenen haberler otomatik elenir.
