# DATAFLOW Millionaire — Master Architecture Document

> Version 1.1 | April 29, 2026
> Status: **v0.1.0 SHIPPED** as a Claude SKILL.md (no React, no web app).
> See `CHANGELOG.md` for ship notes. Original v1.0 spec preserved below for history.

---

## Concept

A roguelike learning game that teaches DATAFLOW pipeline concepts through a Who Wants to Be a Millionaire money ladder, Street Fighter 2 character selection, Slay the Spire path mechanics, and Unreal Tournament streak announcements.

**Core philosophy:** Zero friction. Every second not spent answering questions is wasted time. Minimalism is the design principle.

**The addiction loop:**
- Simple to enter (paste save card, pick character, answer questions)
- Deep to master (upgrade combos, character synergies, path strategy)
- Always fresh (generated questions, random paths, variable rewards)
- Always progressing (bank grows, titles upgrade, weak spots shrink)

---

## The Learning Foundation

All questions are grounded in the **DATAFLOW framework**:

| Letter | Stage |
|---|---|
| D | Define |
| A | Acquire |
| T | Tidy |
| A | Archive |
| F | File |
| L | Launch |
| O | Observe |

Questions are **AI-generated every session** — never the same run twice. Hard questions are application-based ("what breaks if..."), not definition-based. Trick questions allowed but must be instructively wrong — wrong answers teach something.

---

## Game Structure

### Session Flow
1. Paste save card (or start fresh)
2. Character select screen (SF2 style)
3. Path selection (Slay the Spire style)
4. Warm up round (free, no money)
5. Main run — 20 questions, money ladder
6. Bonus stages between rounds (SF2 style)
7. Session end — weak spots review (brief)
8. Upgrade store
9. New save card generated

### The Money Ladder (20 Questions)
```
Q1  — $100
Q2  — $200
Q3  — $300
Q4  — $500
Q5  — $1,000     ⭐ SAFE HAVEN
Q6  — $2,000
Q7  — $4,000
Q8  — $8,000
Q9  — $16,000
Q10 — $32,000    ⭐ SAFE HAVEN
Q11 — $64,000
Q12 — $125,000
Q13 — $250,000
Q14 — $500,000
Q15 — $600,000
Q16 — $650,000
Q17 — $700,000
Q18 — $750,000
Q19 — $900,000
Q20 — $1,000,000 🏆 THUNDER GUN
```

### Question Format by Round
- **Early (Q1-7)** — True/False + 2-choice MC, grouped by DATAFLOW topic, definitions
- **Mid (Q8-14)** — 2-4 choice MC, mixed topics, deeper concepts
- **Late (Q15-20)** — Application based, mixed, "what breaks if...", diagnose scenarios
- **Q20 ($1M)** — Free type answer. No options. No lifelines. Pure recall.

### Difficulty Progression
- Questions escalate within the run like Who Wants to Be a Millionaire
- Round 1 questions grouped by topic (build the pattern)
- Round 2-3 questions mixed (test if you own it)

---

## Character Select (Street Fighter 2)

8 characters. Each perk mirrors their fighter DNA.

| Character | Fighter DNA | Perk |
|---|---|---|
| **Ryu** | Balanced, disciplined, pure fundamentals | No bonus, no weakness — start with 1 extra lifeline |
| **Ken** | Aggressive twin — more risk, more flash | Double money but no safe havens |
| **Chun-Li** | Fastest character, speed is her weapon | More time per question |
| **Guile** | Defensive, calculated, waits you out | Extra safe havens at Q3, Q8, Q15 |
| **Blanka** | Unpredictable, wild, electric chaos | Random multiplier every round (1x-3x) |
| **Zangief** | Tank, absorbs punishment | Wrong answer costs nothing once per session |
| **Dhalsim** | Long reach, stretches past obstacles | Skip 2 questions no penalty |
| **E. Honda** | Hundred Hand Slap — relentless repetition | Every 3 correct in a row = bonus $10,000 |

---

## Path Selection (Slay the Spire)

Before each round, choose your route:

| Path | Questions | Money | Risk |
|---|---|---|---|
| 🔥 **Elite** | Harder, application-based | Double money | High |
| 💰 **Normal** | Standard questions | Standard money | Medium |
| 🛡️ **Safe** | Easier questions | Half money | Low |

### Map Nodes (between questions)
- 🔥 **Elite node** — harder question, bigger reward
- 🏪 **Shop node** — spend money on temporary mid-run boosts
- 🛌 **Rest node** — recover one lifeline
- ❓ **Random event** — wild card, anything could happen

---

## Lifelines (3 per run)

| Lifeline | What it does |
|---|---|
| **50/50** | Removes two wrong answers |
| **Phone a Friend** | I give you a hint |
| **Ask the Audience** | I tell you what most people get wrong on this question |

- Lifelines **reset every session** (do not carry over in save card)
- Extra Lifeline upgrade adds +1 at session start

---

## Streak System (Unreal Tournament)

Correct answer streaks trigger announcements + money multipliers:

| Streak | Announcement | Multiplier |
|---|---|---|
| 2 | **"Double!"** | 1.5x |
| 3 | **"Triple!"** | 2x |
| 4 | **"Quadruple!"** | 2x |
| 5 | **"Rampage!"** | 2.5x |
| 7 | **"Dominating!"** | 3x |
| 9 | **"Unstoppable!"** | 4x |
| 20 | **"GODLIKE!"** | 5x everything |

Break the streak = silence. The silence hits harder than any wrong answer sound.

---

## Bonus Stages (SF2 Between Rounds)

Pure upside — no risk, just opportunity.

| Bonus Stage | Challenge | Reward |
|---|---|---|
| 🚗 **Car Smash** | 5 true/false in 30 seconds | $25,000 perfect / $10,000 partial |
| 🛢️ **Barrel Break** | Define 3 terms back to back, no options | $25,000 perfect / $10,000 partial |
| ✈️ **Plane Bonus** | Explain one concept Feynman style | $25,000 perfect / $10,000 partial |

Character bonuses apply:
- Honda gets double rewards on Barrel Break
- Chun-Li gets extra time on Car Smash
- Blanka gets random bonus stage assigned

---

## Visual Feedback

| Event | Visual |
|---|---|
| Correct answer | Claude logo **POW!!** |
| Wrong answer | **DIZZY!!** stars spinning |
| Safe haven reached | **K.O.!!** — you survived |
| $1M correct | **PERFECT!!** green text |
| Going broke | **GAME OVER** continue countdown |
| Streak | POW!! gets bigger each level |

---

## Upgrade Store (End of Session Only)

Spend banked money on permanent upgrades. Upgrades lost if you go broke.

| Upgrade | Cost | Effect |
|---|---|---|
| **Extra Lifeline** | $50,000 | +1 lifeline next session |
| **Safe Haven Shield** | $100,000 | Adds a 3rd safe haven |
| **Skip Question** | $75,000 | Skip one question no penalty |
| **Double Money Round** | $150,000 | Next session all prizes doubled |
| **Weak Spot Eraser** | $200,000 | Remove one item from weak spots list |
| **Question Preview** | $25,000 | See category before question appears |
| **Second Chance** | $500,000 | Survive one wrong answer |

### Upgrade Combos (Morrowind spell stacking)
- **Double Money Round + Safe Haven Shield** → massive earnings protected
- **Extra Lifeline + Second Chance** → nearly unkillable run
- **Question Preview + 50/50** → dominant early rounds

---

## Title System (Name Color Progression)

| Level | Title | Color |
|---|---|---|
| 0 | Pipeline Rookie | 🟢 Green |
| 1 | Data Wrangler | 🔵 Blue |
| 2 | Pipeline Engineer | 🟡 Yellow |
| 3 | Data Architect | 🟣 Purple |
| 4 | DATAFLOW Master | 🟠 Gold |

*Title progression requirements: TBD based on cumulative earnings + sessions played*

---

## Save Card (Morrowind Character Sheet)

Generated at end of every session. Paste at start of next session to restore full game state.

```
--- DATAFLOW MILLIONAIRE SAVE ---
Player: [NAME]
Title: [TITLE] [COLOR EMOJI]
Character: [SF2 CHARACTER]
Bank: $[AMOUNT]
Streak Record: [BEST STREAK THIS SESSION]
Upgrades Owned: [LIST]
Weak Spots: [LIST]
Concepts Mastered: [LIST]
All Time Best: $[AMOUNT] (Q[NUMBER] - [DATE])
Sessions Played: [NUMBER]
Last Session Earnings: $[AMOUNT]
--- END ---
```

### Going Broke
- Titles intact — earned through knowledge not money
- Upgrades lost — bought with money that's gone
- Bank resets to $1,000 — enough to feel the loss, not start from zero
- Weak spots stay — knowledge gaps don't disappear

---

## Multiplayer (Future — Door Left Open)

**Insert Coin screen** — Street Fighter 2 arcade aesthetic
- "INSERT COIN 25¢" flashing
- Player 1 / Player 2 slots
- Same question set, race to answer faster
- Shared leaderboard

*Not in Version 1. Architecture designed to support it later.*

---

## Build Stages (Version 1)

Build in order. Each stage is a playable checkpoint.

| Stage | What Gets Built | Playable? |
|---|---|---|
| **Stage 1** | Question engine + money ladder + basic UI | ✅ Yes |
| **Stage 2** | SF2 character select + perks | ✅ Yes |
| **Stage 3** | Upgrade store + save card generation | ✅ Yes |
| **Stage 4** | Streak announcer + POW!! animations | ✅ Yes |
| **Stage 5** | Weak spots review + session end screen | ✅ Yes |

If session cuts off — note which stage is complete. New session: paste GitHub link + "continue from Stage X."

---

## Resume Protocol

If compute runs out mid-build:
1. Note which stage was last completed
2. Start new conversation
3. Share this GitHub link
4. Say: "Continue building dataflow-millionaire, Stage X is complete"
5. Build resumes from exact checkpoint

---

## Tech Stack (Version 1) — UPDATED 2026-04-29

**Pivoted from React → SKILL.md** during v0.1.0 build (user constraint: "not a web app").

- **SKILL.md as game engine** — Claude reads instructions, runs the game in conversation
- **ASCII art + emoji blocks** for visual feedback (replaces POW!! / DIZZY!! image renders)
- **AI-generated questions** per session (Claude as the question engine, no external API)
- **In-memory state** during a session
- **Save card** (markdown block) for persistence between sessions
- No database, no hosting, no backend, no React, no animations

Original v1.0 plan (React artifact in Claude chat) preserved below for history.

---

## Version 2 (Future)

- Claude Code full web app
- Real database (SQLite or Supabase)
- Actual SF2 sprite animations
- Sound effects (UT announcer, SF2 sounds)
- Multiplayer lobby
- Slay the Spire path map visual
- Full character artwork
- Mobile responsive

---

## Open Questions — RESOLVED 2026-04-29

- [x] **Title progression** — earnings AND sessions, both must clear (not OR). Thresholds: $10k+3, $100k+10, $1M+25, $10M+50.
- [x] **Multiples of same upgrade?** — No. One of each. Keeps store clean and decisions sharp.
- [x] **Question bank vs AI-gen?** — Pure AI-gen v0.1. v0.2 adds optional bank populated from StrataScratch wins.
- [x] **(Implicit, surfaced during build)** — "React artifact" → ASCII art + emoji blocks. Resolved by user constraint "not a web app."

---

*This document is the single source of truth. Update it as decisions are made. Push to GitHub after every major change.*
