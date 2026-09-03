# MoneyPrinterTurbo Kurulum ve Kullanım Rehberi

**MoneyPrinterTurbo**, konu veya anahtar kelimeden yola çıkarak AI destekli kısa video (Shorts / Reels / TikTok) üreten açık kaynaklı bir video otomasyon aracıdır.

- **Dizin:** `/home/kscmrt/MoneyPrinterTurbo`
- **Sanal Ortam:** `/home/kscmrt/MoneyPrinterTurbo/.venv` (Python 3.11, `uv`)
- **Konfigürasyon:** `/home/kscmrt/MoneyPrinterTurbo/config.toml`

## Temel Yetenekler & Mimari

1. **Senaryo Üretimi (LLM):** OpenAI, Moonshot, Gemini, LiteLLM, Ollama, DeepSeek vb.
2. **Seslendirme (TTS):** Edge-TTS (Ücretsiz), Azure Speech, Google Gemini, MiniMax, ElevenLabs vb.
3. **Görsel / Video Materyal:** Pexels, Pixabay, Coverr, OFox, MiniMax H3, Yerel dosyalar (`--video-source local`).
4. **Altyazı & Senkronizasyon:** Faster-Whisper, font ve stil özelleştirmeleri (altın oran güvenli bölge pozisyonlaması).
5. **Çıktı & Dağıtım:** 9:16 (dikey), 16:9 (yatay), 1:1 (kare) video montajı (MoviePy/FFmpeg tabanlı) ve opsiyonel sosyal medya dağıtımı.

## Çalıştırma Komutları

### 1. WebUI Başlatma (Streamlit Arayüzü)
```bash
cd /home/kscmrt/MoneyPrinterTurbo
sh webui.sh
# veya dış ağa açmak için:
# MPT_WEBUI_HOST=0.0.0.0 sh webui.sh
```
Varsayılan adres: `http://127.0.0.1:8501`

### 2. CLI ile Video Üretme
```bash
cd /home/kscmrt/MoneyPrinterTurbo
./.venv/bin/python cli.py --video-subject "Konu Başlığı" --video-aspect 9:16
```

### 3. API Sunucusu (FastAPI)
```bash
cd /home/kscmrt/MoneyPrinterTurbo
./.venv/bin/python main.py
```
Docs: `http://127.0.0.1:8080/docs`
