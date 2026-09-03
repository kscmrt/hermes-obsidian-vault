# 🎬 Stickman Video Director (Kaomei Workflow)

**Tarih:** 2026-09-02  
**Kaynak Repo:** `https://github.com/kaomei/stickman-video-director`  
**Konum:** `/home/kscmrt/stickman-video-director/`  
**Skill Konumu:** `/home/kscmrt/.hermes/skills/directing-stickman-videos/`  

## 📌 Sistem Özellikleri & İş Akışı:
Eski python çizim motoru yerine artık doğrudan bu repo ve skill kullanılacak.

1. **Giriş:** Metin, konu veya makale.
2. **Setup Gate:** Format (`16:9`, `9:16`, `1:1`) + Tema (`Light`: Beyaz zemin/siyah çöp adam, `Dark`: Siyah zemin/beyaz çöp adam).
3. **Phase A (Yönetmen Teklifi & Storyboard):**
   - 6 sahne (~60 saniye, her klip ~10s).
   - Tam zamanlı görsel hareketler, kamera geçişleri, vurgu renkleri (vivid red, electric blue vb.), SFX ve seslendirme metni.
4. **Phase B (Gemini Omni Flash Prompt Paketi):**
   - 6 adet birbirine kilitli, renk kodsuz, metinsiz temiz Gemini AI video istemi.
5. **Seslendirme:** Gemini 2.5 Flash Voice API (`Charon`, `Puck`, `Aoede`, `Fenrir`) ile %100 doğal seslendirme.
