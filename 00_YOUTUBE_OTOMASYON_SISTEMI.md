# YouTube Otonom Video Üretim Sistemi (Shorts + 16:9 Uzun Belgesel)

## 1. Mimari Genel Bakış
- **Shorts Üretimi (9:16)**: 9 kanal için günlük otonom Shorts akışı.
- **Haftalık Uzun Video (16:9 Belgesel & Masterclass)**: Her kanal için haftada 1 adet 16:9 yatay derinlemesine video (5–10 dk).
- **Zamanlayıcı Servisi**: `weekly-long-scheduler` (PM2 ID: 15).

## 2. Haftalık Uzun Video Yayın Takvimi
| Gün | Saat | Kanal | Konsept / Format | Ses Modeli |
|---|---|---|---|---|
| **Pazartesi** | 18:00 | **Kanal 1: Haber** | Haftanın En Kritik Gelişmeleri & Derin Analiz | `Fenrir` |
| **Salı** | 18:00 | **Kanal 2: Arıza & Kombi** | Kombi ve Ev Aletleri Masterclass Arıza Rehberi | `Puck` |
| **Çarşamba** | 18:00 | **Kanal 3: Oto & OBD2** | Otomobillerde En Sık Çıkan 5 Kritik Arıza ve Çözümü | `Charon` |
| **Perşembe** | 18:00 | **Kanal 4: Hakkını Bil** | Vatandaşın Bilmesi Gereken 5 Gizli Tüketici Hakkı | `Aoede` |
| **Cuma** | 10:30 | **Kanal 6: Dua Penceresi** | Cuma Özel: Kalbe Huzur ve Şifa Veren Dualar | `Aoede` |
| **Cumartesi** | 18:00 | **Kanal 7: Kadim Kıssalar** | Tarihten Büyük Hükümdarların İbretlik Kıssası | `Charon` |
| **Pazar** | 14:00 | **Kanal 8: Global Dua (EN)** | Peaceful Quranic Healing & Spiritual Reflections | `Charon` |
| **Pazar** | 19:00 | **Kanal 5: Dark Science (EN)**| Declassified Secret Files & Dark Science Experiments | `Charon` |
| **Pazar** | 21:30 | **Kanal 9: Mistik Fısıltı** | Yeni Haftada Burçları Bekleyenler & Zamansız Tarot | `Aoede` |

## 3. Sunucu Koruma & Güvenlik İlkeleri
1. **Tekil Kilit Mekanizması (Mutex)**: `long_render.lock` ile aynı anda asla 2 uzun render çalışmaz; sunucu CPU/RAM taşması önlenir.
2. **Düşük Kaynaklı Render**: Remotion `TMPDIR=/home/kscmrt/tmp`, `--concurrency=2`, `--image-format=jpeg`, `--gl=angle`.
3. **Sıfır Halüsinasyon**: `ai_script_engine.js` `generateLongFormDocuScript` ile doğrulanmış veriler üzerinden 4 ana bölüm (Chapters) kurgusu.
4. **16:9 Landscape B-Roll**: Pexels ve Pixabay üzerinden yatay HD materyal çekimi.
