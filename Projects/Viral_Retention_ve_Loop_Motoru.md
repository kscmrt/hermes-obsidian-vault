# Viral YouTube Shorts Retention & Seamless Loop Motoru (v2.0)

**Tarih:** 2026-09-04  
**Durum:** Aktif & PM2 ile Canlıda

## 1. 1000 İzlenme Eşiğini Kırma Mimarisi

YouTube Shorts algoritmasında tohum kitle testini (%70+ Viewed Rate, %100+ Retention) geçmek için sabit şablon metinler kaldırılmış ve dinamik Gemini AI kurgu motoru (`shared/ai_script_engine.js`) devreye alınmıştır.

### Ana Bileşenler:
1. **0–2 sn Agresif Hook:** Soru, şok edici veri veya "Bunu yapıyorsanız hemen durun / servisi aramayın" uyarısı.
2. **Kusursuz Döngü (Seamless Loop):** Videonun son cümlesi, ilk cümlenin başına gramer ve anlamsal olarak bağlanarak izleyicinin videonun bittiğini anlamadan tekrar izlemesi sağlanır (APV %110+ hedeflenir).
3. **Konuya Özel Mikro B-Roll:** Pexels/Pixabay sorguları statik kalıplar yerine yapay zekanın ürettiği sahneye özel İngilizce terimlerle çekilir.
4. **Etkileşim & Sabit Yorum:** İzleyiciyi ikiye bölen ve tartışma başlatan sorular otomatik olarak videonun altına sabitlenir.

## 2. Entegre Edilen Kanallar
- **Kanal 1 (@cahitx - Haber):** `Fenrir` spiker, 22-26s sıcak gündem kancası, döngülü haber akışı.
- **Kanal 2 (@hatakodu - Arıza):** `Puck` spiker, 0 TL tamir / reset rehberi, acil uyarı kancası.
- **Kanal 3 (@otokod - Oto):** `Charon` spiker, OBD2 sırları, motor arıza ışığı kurgusu.
- **Kanal 4 (@hakkinibil - Tüketici):** `Aoede` spiker, tazminat ve para iadesi kancası.
- **Kanal 6 (@duapenceresi - Dua):** `Aoede` spiker, huşu dolu inşirah kancası ve Amin çağrısı.
- **Kanal 7 (@kadimkissalar - Kıssa):** `Charon` spiker, ibretlik kıssa ve bilgelik dersi.
- **Kanal 8 (@peacefuldua - Global Dua):** `Charon/Christopher` spiker, huzur ve şifa duaları.
