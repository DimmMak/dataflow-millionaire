# dataflow-millionaire — Changelog

## v0.1.0 — 2026-04-29

**First playable.** Translated v1.0 ARCHITECTURE.md (2026-04-13) into a SKILL.md game engine. Pure Claude conversation — no React, no web app, no rendering.

### What's in
- Full game flow: insert coin → save card check → character select → path select → warm-up → 20-Q ladder → end-of-session → upgrade store → save card emit
- 8 SF2 characters with verbatim perks from ARCHITECTURE.md
- 3 Slay-the-Spire paths (Elite / Normal / Safe)
- Money ladder Q1-Q20 with 2 safe havens (Q5, Q10) — Guile gets +3 (Q3, Q8, Q15)
- 7 streak announcements (Double / Triple / Quadruple / Rampage / Dominating / Unstoppable / Godlike)
- 3 lifelines (50/50, Phone a Friend, Ask the Audience)
- 3 bonus stages (Car Smash, Barrel Break, Plane Bonus) at Q5/Q10/Q15
- 7 upgrades (Extra Lifeline, Safe Haven Shield, Skip Question, Double Money Round, Weak Spot Eraser, Question Preview, Second Chance) — one of each, no duplicates
- 5-tier title system with earnings AND sessions thresholds (both must clear)
- ASCII art + emoji blocks for visual feedback (POW!! / DIZZY!! / K.O.!! / GAME OVER)
- Save card markdown format with mid-run resume support
- AI-generated questions per session (no question bank in v0.1)
- Weak-spots logging compatible with `examiner` (shared schema)

### Open questions resolved (from ARCHITECTURE.md line 311-315)
- **Title progression:** earnings AND sessions, both must clear (not OR)
- **Multi-upgrade ownership:** one of each, no duplicates
- **Question bank vs AI-gen:** pure AI-gen v0.1 (v0.2 adds optional bank from StrataScratch wins)
- **"React artifact" → markdown:** ASCII art + emoji blocks (no SVG, no rendered animations)

### Cross-skill composition
- Shares `weak-spots.jsonl` schema with `examiner` — millionaire-misses feed examiner's morning drill weighting
- Auto-suggests `dataflow-tutor` when a DATAFLOW concept hits 3+ misses
- Auto-logs to `notepad` tagged `study,millionaire,dataflow`
- `schedule`-able for weekend morning trigger

### What's NOT in (v0.1 scope cuts)
- Multiplayer (V2 in ARCHITECTURE.md, line 249-257)
- Sound effects (UT announcer, SF2 sounds)
- Real SF2 sprite animations
- Slay the Spire path map visual
- Mobile responsive
- Real database (in-memory state + save card persistence only)

### Why ship at v0.1
- Phase 1 of data analyst training curriculum starts Day 1
- `examiner` ships same day; arcade complement to gym
- Earn-your-features: ship minimum, let real play surface v0.2 priorities
- ARCHITECTURE.md was 70% spec'd already; encoding into SKILL.md was the missing 30%

### Known limits
- AI-gen quality varies; question difficulty calibration on Q15-Q20 is the hardest band to generate consistently
- Wrong-answer-must-teach-something rule is honor-system on Claude's part — no automated check
- Save card forgery checks are sanity-only (bank ≤ sessions × $10M); no cryptographic signing
- Streak announcements assume terminal/chat supports emoji — degrade gracefully to text
