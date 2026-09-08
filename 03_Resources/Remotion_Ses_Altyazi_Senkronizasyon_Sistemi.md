# Remotion Metin & Seslendirme Senkronizasyon Sistemi (Proportional Subtitle Engine)

**Tarih:** 2026-09-08  
**Kapsam:** Remotion Video Motoru (`src/DynamicNews`, `src/ApplianceFix`, `src/CarWarning`, `src/DuaShorts`, `src/KissalarShorts`, `src/GlobalDuaShorts`)

---

## 1. Problem Tespiti (Neden Metin Sesten Önce Gidiyordu?)
1. **Sabit Sahne Bölünmesi (Uniform Scene Duration):** Toplam video karesi (900 frame) sahne sayısına eşit bölünüyordu (`900 / 4 = 225`). Kısa bir kanca cümlesi 2.5 saniyede bitiyor ancak 7.5 saniye ayrılıyordu; uzun bir çözüm cümlesi 8 saniye sürüyorken yine 7.5 saniye ayrılıp spiker bitirmeden diğer sahneye geçiliyordu.
2. **Doğrusal Kelime Grubu Bölünmesi (Linear Chunking):** `WordKaraoke` her 3 kelimelik gruba kelime uzunluğuna ve noktalama duraklamalarına bakmaksızın eşit frame veriyordu. Spiker virgüllerde veya noktalarda duraksadığında altyazı hızla akmaya devam ediyordu.

---

## 2. Uygulanan Çözüm Mimarisi

### A. Orantılı Sahne Süresi Hesaplama (Proportional Scene Timing)
Her sahnenin karesi, metnin karakter sayısı ile noktalama duraklama ağırlıklarının toplam video süresine oranına göre hesaplanır:

$$\text{Weight}_i = \text{Length}(\text{speechText}_i) + (\text{virgüller} \times 8) + (\text{noktalar} \times 14)$$

$$\text{Duration}_i = \text{round}\left(\frac{\text{Weight}_i}{\sum \text{Weights}} \times \text{TotalDurationInFrames}\right)$$

### B. Ağırlıklı Kelime Karaoke Sistemi (Phonetic Pause Weighted Karaoke)
* `WordKaraoke` bileşeni her kelime öbeğini (chunk) içerdiği harf sayısı ve sonundaki noktalama işaretlerine (`.`, `!`, `?`, `,`) göre ağırlıklandırır.
* Cümle sonlarında otomatik olarak ek bekleme süresi tanınır; böylece spiker nefes alırken altyazı spikerin ses hızına tam kilitlenir.

---

## 3. Güncellenen Şablonlar
- `src/DynamicNews/index.tsx` (9 Kanalın tamamında çalışan ana şablon)
- `src/ApplianceFix/index.tsx` (Arıza Kodları kanalı)
- `src/CarWarning/index.tsx` (Otokod kanalı)
- `src/DuaShorts/index.tsx` (Dua Penceresi)
- `src/KissalarShorts/index.tsx` (Kadim Kıssalar)
- `src/GlobalDuaShorts/index.tsx` (Global Peaceful Duas)

Tüm şablonlar test edilmiş ve sıfır derleme hatası ile doğrulanmıştır.
