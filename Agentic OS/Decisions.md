# Decisions Log

Önemli kararlar ve belirlenen kurallar.

## Decision: Hafıza Sistemi Tasarımı - 2026-09-01

**Context:**
- Ben (Murat) otonom AI sistemleri geliştiriyorum
- Her konuşmadan sonra bağlam kayboluyor
- Yeni oturumda her şeyi tekrar anlatmam gerekiyor

**Decision:**
Obsidian vault kullanarak kalıcı hafıza sistemi kuracağım.
- **Why?** Text-based, portable, any agent açabiliyor
- **Structure:** PARA + Agentic OS (9 folders)
- **Rules:** 5 context rules + ownership rule (append only)
- **Git sync:** Daily commits

**Implementation:**
- Protocol.md: Her agent'in okuyacağı ilk şey
- About.md: Benim hakkımda (değerler, setup, iletişim stili)
- Projects/_index.md: Şu anki hedefler
- Agentic OS logs: Her session kaydediliyor

**Next Decision Point:**
Hermes Agent'i vault'a nasıl bağlayacak?
- Option 1: Hermes skill (read vault at start)
- Option 2: Claude Code plugin
- Option 3: Script-based sync

---

**Date:** 2026-09-01 21:45  
**Approved:** Self + Hermes recommendation
