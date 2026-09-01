# Remotion Project Pipelines

Remotion video automation project at `/home/kscmrt/remotion-video/`

## Compositions (React/TypeScript)

**Video Templates:**
- **ApplianceFix** — Appliance malfunction diagnosis videos (Turkish)
- **CarWarning** — Car dashboard warning light explainers (Turkish)
- **DynamicNews** — Dynamic news segments with overlays
- **FinancePulse** — Finance/market update template
- **HakRehberi** — Legal/rights guidance videos
- **MysteryDocu** — Mystery documentary style
- **NewsShorts** — Short-form news clips (parameterized)
- **ProNewsShorts** — Professional news shorts pipeline
- **SaaSPromo** — SaaS product promotion template
- **VersusReview** — Versus/comparison review template

## Automation Scripts

**News Bots:**
- `auto_news_bot.js` — RSS feed → AI script → TTS → Render → Upload
- `autonomous_news_pilot.js` — Advanced news pipeline (Gemini + Pexels)
- `master_news_bot.js` — Master orchestrator (calls sub-modules)

**Voice & TTS:**
- `gen_gemini_voices.js` — Generate voice using Gemini API
- `gen_long_tts.js` — Long-form TTS (splits text)
- `gen_voices.js` — Voice synthesis (MsEdge TTS)

**Rendering:**
- `render_dpf.js` — DPF (car dashboard warning) video render
- `render_emel.js` — Emel-themed video render
- `render_hak.js` — Hak Rehberi video render
- `render_3_formats.js` — Render same content in 3 formats
- `render_pro_news.js` — Pro news shorts render

**Utilities:**
- `download_scenes.js` — Download scene assets
- `dl_bg_video.js` — Download background videos (Pexels)
- `list_rss.js` — List RSS feeds
- `list_voices.js` — List available TTS voices
- `list_models_exact.js` — List Gemini models

## Autopilot Pipelines

**Three parallel autopilot systems:**

### 1. autopilot/ (News Channel)
**Purpose:** Automated news video production  
**Flow:**
```
1. RSS Feed → getNextNewsArticle()
2. Gemini AI → generateShortsScript() (hook, 3 points, SEO)
3. Pexels API → fetchMultipleBackgroundVideos()
4. MsEdge TTS → synthesizeVoice()
5. Remotion → Render video
6. YouTube → uploadToYouTube()
```
**Stage Tracking:** `live_state.json` (real-time progress)
**Output:** `output/[timestamp]_[slug]/` with audio + metadata

### 2. autopilot-ariza/ (Appliance Malfunction)
**Purpose:** Turkish appliance repair diagnosis videos  
**Channels:** Bosch, Vestel, ECA, Demirdöküm (appliances + combis)  
**Key File:** `fault_generator.js` — generates fault scenarios

### 3. autopilot-oto/ (Car Warnings)
**Purpose:** Turkish car dashboard warning explanations  
**Channels:** Motor arızası, DPF, EPC, TPMS, ABS/ESP, Şarj, Isı  
**Key File:** `car_fault_generator.js` — generates warning scenarios

## Data Flow

```
Stage 1: Content Generation
  ↓ RSS → Gemini AI Script → (hook + 3 bullets + SEO keywords)
  
Stage 2: Assets
  ↓ Pexels API → Background videos (scene_1, 2, 3, 4)
  ↓ MsEdge TTS → Voice narration (45-60s)
  
Stage 3: Composition
  ↓ Remotion component (NewsShorts, CarWarning, etc.)
  ↓ Props: scenes + audio + text overlays
  
Stage 4: Render
  ↓ ffmpeg → MP4 (1080p, H.264, AAC)
  
Stage 5: Publish
  ↓ YouTube OAuth → Upload with title + description + tags
  ↓ Monitor upload status
```

## Configuration Files

- `package.json` — Node dependencies (Remotion, Gemini, Pexels, YouTube API)
- `remotion.config.ts` — Remotion composition defaults
- `config.json` (autopilot/) — Channel config, upload schedule
- `db/seen_news.json` — RSS feed tracking (avoid duplicates)
- `db/seen_oto.json`, `db/seen_faults.json` — Per-channel history

## API Keys Used

- **Gemini API** — Script generation (3.5/3.7 models)
- **Pexels API** — Background video clips
- **YouTube OAuth** — Video upload + channel management
- **MsEdge TTS** — Turkish voice synthesis (free)

## Key Features

✅ **Autonomous** — Runs on schedule (cron)  
✅ **Parallelization** — 3 independent autopilot systems  
✅ **Error Handling** — Timeout protection, fallback voices  
✅ **State Tracking** — `live_state.json` for monitoring  
✅ **Zero-Cost TTS** — MsEdge (free), no subscription  
✅ **Multilingual** — Turkish primary, English support  
✅ **SEO-Aware** — Gemini generates keywords + descriptions  

## Next Steps

- Monitor autopilot runs (check `live_state.json`)
- Update RSS feed sources (db/seen_*.json)
- Adjust Remotion component parameters (src/*/)
- Scale to additional channels (create new autopilot-*)

---
**Last Updated:** 2026-09-01
**Status:** ✅ Operational (news autopilot ready)
