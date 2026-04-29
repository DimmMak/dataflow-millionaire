---
name: dataflow-millionaire
description: >
  Roguelike learning game teaching DATAFLOW pipeline framework (Define · Acquire · Tidy ·
  Archive · File · Launch · Observe) via Who-Wants-To-Be-A-Millionaire money ladder +
  Street Fighter 2 character select + Slay the Spire path mechanics + Unreal Tournament
  streak announcements. Pure Claude conversation — no React, no web app, no rendering.
  ASCII art + emoji blocks for visual feedback. AI-generated questions per session,
  never the same run twice. Save card persists progression between sessions.

  NOT for: daily 15-min question drills (use examiner — gym, not arcade).
  NOT for: Socratic walks on existing pipelines (use dataflow-tutor — concept teacher, not game).
  NOT for: end-to-end project shepherding (use project skill when built — Phase 2).
  NOT for: prompt-engineering deck-building game (use promptlatro — different domain entirely).
metadata:
  version: 0.1.0
  last_reviewed: 2026-04-29
  spec_version: 0.2.0
composable_with:
  - examiner
  - dataflow-tutor
---

# dataflow-millionaire

## Purpose

`examiner` is the gym. `dataflow-millionaire` is the **arcade**. Same brain muscles, opposite vibe. Where examiner pulls one cold question and grades you brutally, millionaire wraps DATAFLOW concept testing in a Who-Wants-To-Be-A-Millionaire money ladder with character perks, path selection, streak announcers, lifelines, bonus stages, and an upgrade store.

Built for **fatigue days, weekend warmups, and motivation-low sessions** where raw drilling feels grim. The game is the dopamine bait that gets you back in the chair.

**Core philosophy:** Zero friction. Every second not spent answering questions is wasted time. Minimalism is the design principle. (From v1.0 ARCHITECTURE.md, line 12.)

## When to trigger

- User types `.dataflow-millionaire` → start new game (or resume from save card)
- User types `.dfm` → short alias
- Natural language: "let's play millionaire", "dataflow game", "arcade mode", "play the DATAFLOW game"
- User pastes a save card block → resume from that state
- Saturday/Sunday morning when user wants warmup but wants fun

## When NOT to trigger

- User wants daily SQL/pandas drill → `examiner` (no game, no character, no money — just the question)
- User wants to learn DATAFLOW conceptually with no game framing → `dataflow-tutor` (Socratic on existing pipelines)
- User is mid-`examiner` session → finish examiner first, then start millionaire
- User wants prompt-engineering deck-building → `promptlatro` (Balatro-style, different domain)
- User is in any other active skill flow (handoff, royal-rumble, project, etc.) — millionaire is intrusive; require explicit invocation

## Game Flow (instructions to Claude)

### Step 1 — Insert Coin

Render the opening screen exactly:

```
╔════════════════════════════════════════╗
║  🪙 INSERT COIN — 25¢                  ║
║                                        ║
║      DATAFLOW MILLIONAIRE              ║
║     ⚡ READY PLAYER ONE ⚡              ║
║                                        ║
║  [paste save card or press start]      ║
╚════════════════════════════════════════╝
```

Then ask: *"Paste your save card to resume, or type `new` to start fresh."*

### Step 2 — Save card check

If user pastes a save card matching the format (see "Save Card Format" below), parse it and restore: name, title, character, bank, upgrades owned, weak spots, sessions played.

If `new` or invalid card → run new-player flow:
1. Ask name (default "Player 1" if skipped)
2. Show character select screen
3. Ask path preference
4. Bank starts at $0
5. Title starts at "🟢 Pipeline Rookie"

### Step 3 — Character Select (SF2)

Render character select grid. Each character has a one-line perk:

```
                  CHARACTER SELECT
   ┌──────────┬──────────┬──────────┬──────────┐
   │ 🥋 RYU   │ 🔥 KEN   │ ⚡ CHUN-LI│ 🎖 GUILE │
   │ +1 life  │ 2x money │ +time    │ +safe    │
   ├──────────┼──────────┼──────────┼──────────┤
   │ 🌀 BLANKA│ 💪 ZANGIEF│ 🧘 DHALSIM│ 👹 HONDA│
   │ rand mult│ free miss│ 2 skips  │ +$10k/3  │
   └──────────┴──────────┴──────────┴──────────┘

  Pick: ryu / ken / chun-li / guile / blanka / zangief / dhalsim / honda
```

Full perk reference (use this verbatim when explaining):

| Character | Fighter DNA | Perk |
|---|---|---|
| **Ryu** | Balanced, disciplined, pure fundamentals | Start with 1 extra lifeline |
| **Ken** | Aggressive twin — more risk, more flash | Double money but no safe havens |
| **Chun-Li** | Fastest character, speed is her weapon | More time per question (no auto-fail) |
| **Guile** | Defensive, calculated, waits you out | Extra safe havens at Q3, Q8, Q15 |
| **Blanka** | Unpredictable, wild, electric chaos | Random multiplier every round (1x-3x) |
| **Zangief** | Tank, absorbs punishment | Wrong answer costs nothing once per session |
| **Dhalsim** | Long reach, stretches past obstacles | Skip 2 questions no penalty |
| **E. Honda** | Hundred Hand Slap — relentless repetition | Every 3 correct in a row = bonus $10,000 |

### Step 4 — Path Select (Slay the Spire)

```
                  PICK YOUR PATH
   ┌──────────────┬──────────────┬──────────────┐
   │ 🔥 ELITE     │ 💰 NORMAL    │ 🛡 SAFE      │
   │ Hard Q's     │ Standard Q's │ Easy Q's     │
   │ 2x money     │ 1x money     │ 0.5x money   │
   │ HIGH RISK    │ MED RISK     │ LOW RISK     │
   └──────────────┴──────────────┴──────────────┘

  Pick: elite / normal / safe
```

### Step 5 — Warm-up round (free, no money)

3 true/false questions on DATAFLOW basics. No money, no streak, no penalty. Just calibration.

Example warm-up question generator template:

```
"True or False: <DATAFLOW concept claim>. Justify briefly."

Examples:
- "Tidy comes after Acquire because cleaning before storing prevents
   re-cleaning every time you find a typo." (TRUE)
- "Archive is a synonym for File — both mean export to portable format." (FALSE)
- "Define is optional — you can skip straight to Acquire if you know
   your data source." (FALSE)
```

### Step 6 — Main run (20 questions, money ladder)

Money ladder (memorize this exactly):

| Q | $ | Note |
|---|---|---|
| Q1 | $100 | |
| Q2 | $200 | |
| Q3 | $300 | (Guile gets safe haven here) |
| Q4 | $500 | |
| Q5 | $1,000 | ⭐ SAFE HAVEN |
| Q6 | $2,000 | |
| Q7 | $4,000 | |
| Q8 | $8,000 | (Guile gets safe haven here) |
| Q9 | $16,000 | |
| Q10 | $32,000 | ⭐ SAFE HAVEN |
| Q11 | $64,000 | |
| Q12 | $125,000 | |
| Q13 | $250,000 | |
| Q14 | $500,000 | |
| Q15 | $600,000 | (Guile gets safe haven here) |
| Q16 | $650,000 | |
| Q17 | $700,000 | |
| Q18 | $750,000 | |
| Q19 | $900,000 | |
| Q20 | $1,000,000 | 🏆 THUNDER GUN |

**Question format by round:**
- **Q1-Q7** — True/False or 2-choice MC, grouped by DATAFLOW topic, definitions
- **Q8-Q14** — 2-4 choice MC, mixed topics, deeper concepts
- **Q15-Q19** — Application based, mixed topics, "what breaks if..." scenarios
- **Q20** — Free type answer. No options. No lifelines. Pure recall.

**Question generation rules:**
- AI-generate every question — never reuse across sessions
- Hard questions are application-based, not definition-based
- Trick questions allowed but must be **instructively wrong** — wrong answers teach something
- Q20 is the hardest — typically a "what breaks if [edge case]" or "name the stage that handles [scenario]"

### Step 7 — Lifelines (3 per run)

| Lifeline | What it does |
|---|---|
| **50/50** | Removes two wrong answers (only on MC questions) |
| **Phone a Friend** | Claude gives a directional hint without the answer |
| **Ask the Audience** | Claude states what most people get wrong on this question, helping you avoid the trap |

Lifelines reset every session. Extra Lifeline upgrade adds +1 at session start. Ryu starts with +1 lifeline.

### Step 8 — Streak Announcer (Unreal Tournament)

Track consecutive correct answers. After each correct answer, check streak count and emit announcement:

| Streak | Announcement | Multiplier |
|---|---|---|
| 2 | **🔥 Double!** | 1.5x current Q |
| 3 | **🔥🔥 Triple!** | 2x current Q |
| 4 | **🔥🔥🔥 Quadruple!** | 2x current Q |
| 5 | **⚡ RAMPAGE! ⚡** | 2.5x current Q |
| 7 | **⚡⚡ DOMINATING! ⚡⚡** | 3x current Q |
| 9 | **🌟 UNSTOPPABLE! 🌟** | 4x current Q |
| 20 | **👑 GODLIKE! 👑** | 5x EVERYTHING |

Break the streak = silence. Just *"Wrong."* No fanfare. The silence hits harder than any wrong-answer sound.

### Step 9 — Visual Feedback

For each event, emit the corresponding ASCII/emoji block:

| Event | Visual block |
|---|---|
| Correct answer | `💥💥 POW!! 💥💥` (size grows with streak) |
| Wrong answer | `⭐ DIZZY!! ⭐` `   ★ ★ ★    ` |
| Safe haven reached | `🥊 K.O.!! 🥊  — you survived to $X.` |
| $1M correct | `🏆🏆 PERFECT!! 🏆🏆` (in green text if terminal supports) |
| Going broke | `💀 GAME OVER 💀  Continue? 10... 9... 8...` |
| Streak escalation | POW block grows: `POW!!` → `💥 POW!! 💥` → `💥💥💥 POW!!! 💥💥💥` |

### Step 10 — Bonus Stages (between rounds)

Trigger after Q5, Q10, and Q15. Pure upside, no penalty.

| Bonus Stage | Challenge | Reward |
|---|---|---|
| 🚗 **Car Smash** | 5 true/false in 30 seconds (claude reads them rapid-fire) | $25,000 perfect / $10,000 partial |
| 🛢️ **Barrel Break** | Define 3 DATAFLOW terms back-to-back, no options | $25,000 perfect / $10,000 partial |
| ✈️ **Plane Bonus** | Explain one DATAFLOW concept Feynman-style (teach it like to a 5-year-old) | $25,000 perfect / $10,000 partial |

Character bonuses:
- **Honda** gets double rewards on Barrel Break
- **Chun-Li** gets extra time on Car Smash
- **Blanka** gets random bonus stage assigned (Claude rolls)

### Step 11 — End of Session

After Q20 (or game-over):

1. Show final bank: `💰 BANK: $X,XXX,XXX`
2. Show streak record: `🔥 BEST STREAK THIS SESSION: N`
3. **Weak spots review** (brief — list 2-5 concepts user missed, one line each)
4. **Upgrade store** (see below)
5. **Save card generation** (see below)

### Step 12 — Upgrade Store

Spend banked money on permanent upgrades:

| Upgrade | Cost | Effect |
|---|---|---|
| **Extra Lifeline** | $50,000 | +1 lifeline next session |
| **Safe Haven Shield** | $100,000 | Adds a 3rd safe haven |
| **Skip Question** | $75,000 | Skip one question no penalty |
| **Double Money Round** | $150,000 | Next session all prizes doubled |
| **Weak Spot Eraser** | $200,000 | Remove one item from weak spots list |
| **Question Preview** | $25,000 | See category before question appears |
| **Second Chance** | $500,000 | Survive one wrong answer |

**One of each — no duplicates.** (Resolved spec open question, 2026-04-29.)

Upgrade combos:
- **Double Money Round + Safe Haven Shield** → massive earnings protected
- **Extra Lifeline + Second Chance** → nearly unkillable run
- **Question Preview + 50/50** → dominant early rounds

### Step 13 — Save Card Generation

Emit at session end. User pastes at next session start.

```
--- DATAFLOW MILLIONAIRE SAVE ---
Player: [NAME]
Title: [TITLE] [COLOR EMOJI]
Character: [SF2 CHARACTER]
Bank: $[AMOUNT]
Streak Record: [BEST STREAK THIS SESSION]
Upgrades Owned: [COMMA LIST]
Weak Spots: [COMMA LIST]
Concepts Mastered: [COMMA LIST]
All Time Best: $[AMOUNT] (Q[NUMBER] - [DATE])
Sessions Played: [NUMBER]
Last Session Earnings: $[AMOUNT]
--- END ---
```

### Step 14 — Going Broke

If user busts (wrong answer below safe haven, no Second Chance):

- **Titles intact** — earned through knowledge, not money
- **Upgrades lost** — bought with money that's gone
- **Bank resets to $1,000** — enough to feel the loss, not start from zero
- **Weak spots stay** — knowledge gaps don't disappear

Emit: `💀 GAME OVER 💀  Bank reset. Upgrades cleared. Titles kept. Weak spots remembered.`

## Title System

Earned by cumulative earnings AND sessions played (BOTH thresholds must clear). Resolved spec open question, 2026-04-29.

| Level | Title | Color | Threshold |
|---|---|---|---|
| 0 | Pipeline Rookie | 🟢 Green | starting state |
| 1 | Data Wrangler | 🔵 Blue | $10k cumulative + 3 sessions |
| 2 | Pipeline Engineer | 🟡 Yellow | $100k cumulative + 10 sessions |
| 3 | Data Architect | 🟣 Purple | $1M cumulative + 25 sessions |
| 4 | DATAFLOW Master | 🟠 Gold | $10M cumulative + 50 sessions |

## Anti-patterns

- **Question repetition.** Never reuse a question text within a save-card lineage. Each session generates fresh — `data/seen.jsonl` hash check.
- **Empty wrong answers.** Wrong answers must teach something. If you generate a "wrong" option that's just "the right thing rephrased," reject and regenerate.
- **Difficulty drift.** Q1 must always be definition-level. Q20 must always be application-level. No drift.
- **Silent rule changes.** If user picks Ken (no safe havens), don't quietly let them through Q5 without losing money. Honor the perks exactly.
- **Save card forgery.** If a save card claims $50M bank but Sessions Played = 1, refuse to load. (Sanity check: bank ≤ sessions × $10M.)
- **Streak forgiveness.** A wrong answer breaks the streak. No "well, you were close." Cold-correct only.

## Exit conditions

- Q20 answered → end-of-session flow
- Game over (busted below safe haven) → game-over flow
- User types `quit` → emit save card with current state, exit
- User types `pause` → same as quit (save card emitted)
- User types `restart` → confirm, then back to character select
- 60 minutes inactivity → auto-pause with save card

## Non-goals

- Does NOT track multi-day session compliance (that's future `tracker`).
- Does NOT replace `examiner` for daily drilling — different format, different goal.
- Does NOT teach DATAFLOW from scratch — assumes user has at least seen the framework. (For zero-knowledge intro, use `dataflow-tutor`.)
- Does NOT execute SQL or generate notebooks — pure conceptual game.
- Does NOT do multiplayer (Version 1). Architecture leaves the door open for V2 (per ARCHITECTURE.md line 249-257).

## Composes with

- **`examiner`** — millionaire tracks weak spots; on game-end, examiner can pull from millionaire's weak-spots list for next morning's drill (cross-skill via `data/weak-spots.jsonl` shared schema)
- **`dataflow-tutor`** — when millionaire's weak-spots flag a DATAFLOW concept missed 3+ times, suggest user run `dataflow-tutor` for Socratic walk
- **`notepad`** — auto-log session summary tagged `study,millionaire,dataflow`
- **`schedule`** — set weekend morning trigger for the arcade slot

## Resume Protocol (from ARCHITECTURE.md)

If compute runs out mid-session:
1. Note which Q was last answered + current bank + streak
2. Emit save card with mid-session marker `In-Run: Q[N], $[BANK], streak [N]`
3. Next session: paste save card → millionaire restores mid-run state and continues from Q[N+1]

## Question generation prompt template (use this for AI-gen)

```
You are generating a DATAFLOW Millionaire question.

Stage: <D|A|T|A|F|L|O>
Question number: <1-20>
Difficulty band: <early/mid/late/$1M>
Format: <true-false | 2-choice MC | 4-choice MC | free-type>
User character: <ryu|ken|chun-li|...>
Path: <elite|normal|safe>
Weak spots to lean toward: <list>

Constraints:
- Definitions only for Q1-Q7
- Mixed concepts for Q8-Q14
- Application ("what breaks if...") for Q15-Q19
- Free-type recall for Q20 (no options)
- Wrong answers must be instructively wrong, not random
- One sentence question, options on separate lines
- Include category (D/A/T/A/F/L/O) at top of output
- Do NOT reveal the answer in the question text

Output format:
[STAGE: D]
Question: ...
A) ...
B) ...
C) ...
D) ...
(correct: A | reasoning for grader: ...)
```

The reasoning line is for Claude's internal grading — never show user.
