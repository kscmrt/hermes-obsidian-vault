# Autopilot Audit & Improvement Plan

## Issues Found

### 🔴 CRITICAL
1. **API Keys Hardcoded** — config.json içinde Gemini + Pexels keys exposed
2. **No .env Support** — Production-unsafe
3. **Clone Voice Dependency** — `/home/kscmrt/coqui-env/bin/python3` hardcoded (may not exist)
4. **YouTube Token Manual** — Requires manual OAuth setup (client_secret.json)

### 🟡 MEDIUM
1. **No Error Recovery** — If Gemini/Pexels fail, cascade fails
2. **Voice Synthesis Lock** — CPU lock file primitive (can deadlock)
3. **Render Integration Missing** — Scripts generate assets but don't trigger Remotion render
4. **No Async Parallelization** — Sequential processing (slow for 4 daily videos)
5. **Hardcoded Paths** — `/home/kscmrt/remotion-video/` scattered throughout

### 🟢 MINOR
1. **Logging** — Not structured (timestamp + level)
2. **Monitoring** — live_state.json is manual JSON (no DB)
3. **Config Validation** — No startup validation
4. **Retry Logic** — Basic (3 retries), no exponential backoff

## Improvements to Implement

### Phase 1: Security + Configuration
- [ ] Create `.env` file for all secrets
- [ ] Update all modules to read from `.env` (dotenv package)
- [ ] Remove hardcoded paths → use environment variables
- [ ] Add `.env.example` to repo (for documentation)
- [ ] Validate all config on startup

### Phase 2: Reliability
- [ ] Add fallback chains (Gemini fail → re-try older model; Pexels fail → Archive.org)
- [ ] Implement exponential backoff for API calls
- [ ] Add circuit breaker pattern
- [ ] Better error logging (file + console)

### Phase 3: Integration
- [ ] Connect to Remotion render pipeline (call `remotion render` after assets generated)
- [ ] Add Backlot status update (send output to live_state + Backlot API)
- [ ] Implement job queue (BullMQ or simple JSON queue)

### Phase 4: Performance
- [ ] Parallelize: asset fetch + script generation can run together
- [ ] Add caching (RSS parse results, Pexels searches)
- [ ] Implement pub/sub for inter-process communication

### Phase 5: Monitoring
- [ ] Replace live_state.json with proper logging
- [ ] Add Prometheus metrics (videos/day, success rate, API latency)
- [ ] Email alerts on failures

## Quick Wins (Do First)

1. **Create .env** (5 min)
2. **Add dotenv** to package.json (1 min)
3. **Refactor config reads** (30 min)
4. **Add fallback chains** (45 min)
5. **Connect to render** (60 min)
6. **Test end-to-end** (30 min)

---

**Execution Plan:**
1. Audit complete ✓
2. Create improved autopilot_v2.js with all fixes
3. Test with dry-run
4. Run one cycle
5. Verify YouTube upload
