# Agent Protocol File

**Bu dosya her agent'in okuyacağı ilk şeydir.**

## Context Read Order (İşe başlamadan önce)
1. **About.md** oku (kim ben, ne işim)
2. **Projects/_index.md** oku (şu anki hedefler)
3. **Areas/_index.md** oku (uzun vadeli focus)
4. **Relevant wiki pages** arat (varsa)

## Five Context Rules (ÖNEMLİ!)

### Rule 1: Search Before Guessing
Eğer bir soruya cevap vermem gerekiyorsa önce vault'ta arat.  
Bulduğum bilgiyi kaynak belirterek kullan.

### Rule 2: List Your Sources
Cevapımda kullandığım her not'u isimle saydığım:
> Used: About.md, Projects/Agent-OS, Wiki/Hermes

### Rule 3: Admit Silence
Eğer vault'ta cevap yoksa, **invented** etme.  
Düz söyle: "Vault'ta bu konu yok, tahmin yapıyorum:"

### Rule 4: Date Everything
Her yeni nota tarih ekle:
```
Timestamp: 2026-09-01 21:45
```

### Rule 5: Grounded Not Guessing
Eğer About.md'de "sıfır-maliyetli üretim" yazıyorsa,  
hiçbir paid API'yi teklif etme.  
Eğer "otonomik çalışma" yazıyorsa, interaktif prompts sorma.

---

## Ownership Rule (HEP APPEND, ASLA DELETE)

**KURAL:** Yeni notlar altına eklenecek. Eski notlar asla silinmeyecek.

Doğru:
```
## Old note (kept)
old content

## New entry - 2026-09-01
new content
```

Yanlış:
```
## Old note (DELETED)
## New note (replaces old)
```

Her agent kendi klasörü:
- Hermes → `/Agentic OS/Hermes_Log.md`
- Claude → `/Agentic OS/Claude_Log.md`
- OpenCode → `/Agentic OS/OpenCode_Log.md`

---

## Write Before You Leave

İşim bittiğinde:
1. Sonuç yaz → `/Agentic OS/[Agent]_Log.md`
2. Eğer decision aldı → `/Agentic OS/Decisions.md` append
3. Eğer workflow buldu → `/Agentic OS/Workflows.md` append
4. Git commit et

Örnek entry:
```markdown
## Session: Agent OS Setup - 2026-09-01 21:45

**Goal:** Hermes vault protocol oluştur

**Completed:**
- Vault folder structure created (PARA + Agentic OS)
- About.md, Projects, Areas created
- Protocol file drafted
- Git initialized

**Decision:** Continue with Obsidian setup next

**Sources Used:** 
- agentos.guide/hermes-second-brain
- agentos.guide/ai-agent-os
```

---

## Map (Hızlı Bulma)

Sık sorular → hangi dosyada:
- "Benim projelerim neler?" → Projects/_index.md
- "Türkçe/İngilizce tercihim?" → About.md
- "Sıfır-maliyetli midir?" → About.md
- "Son kararlar neler?" → Agentic OS/Decisions.md
- "Daha önce ne yaptık?" → Agentic OS/[Agent]_Log.md

---

**Protocol Create Date:** 2026-09-01 21:45  
**Last Updated:** 2026-09-01 21:45
