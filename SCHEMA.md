# dataflow-millionaire — Schemas

> Save card format and JSONL schemas for game state persistence.

---

## Save card (markdown block)

The save card is a human-readable, paste-able block. NOT JSON. Designed so the user can edit it manually if needed and so future-Claude can parse it from a fresh chat.

```
--- DATAFLOW MILLIONAIRE SAVE ---
Player: Danny
Title: Data Wrangler 🔵
Character: Ryu
Bank: $42,500
Streak Record: 7
Upgrades Owned: Extra Lifeline, Question Preview
Weak Spots: Tidy-vs-Archive, Launch-version-control
Concepts Mastered: Define-objective, Acquire-source, File-portable-format
All Time Best: $125,000 (Q12 - 2026-04-22)
Sessions Played: 4
Last Session Earnings: $42,500
In-Run: none
--- END ---
```

### Field reference

| Field | Required | Format | Notes |
|---|---|---|---|
| `Player` | R | string | user-chosen name |
| `Title` | R | `<title> <emoji>` | one of the 5 titles + matching emoji |
| `Character` | R | enum | `Ryu` / `Ken` / `Chun-Li` / `Guile` / `Blanka` / `Zangief` / `Dhalsim` / `Honda` |
| `Bank` | R | `$N,NNN` or `$N,NNN,NNN` | comma-separated thousands, dollar prefix |
| `Streak Record` | R | int | best streak this session (resets each session) |
| `Upgrades Owned` | R | comma list | empty = `none` |
| `Weak Spots` | R | comma list | concepts missed 3+ times historically |
| `Concepts Mastered` | R | comma list | concepts answered correctly 3+ times |
| `All Time Best` | R | `$N (Q# - YYYY-MM-DD)` | best single-session result |
| `Sessions Played` | R | int | total completed sessions |
| `Last Session Earnings` | R | `$N` | earnings of most recent session |
| `In-Run` | R | `none` / `Q# $bank streak#` | mid-session resume marker |

### Validation rules

- **Bank cap sanity:** bank ≤ Sessions Played × $10M (rejects forged cards)
- **Title-threshold consistency:** if Title says `Pipeline Engineer`, cumulative earnings must clear $100k AND sessions ≥ 10
- **Character spelling:** case-insensitive but must match one of 8 names exactly (no typos accepted)
- **Empty list convention:** `none` (not blank, not `-`, not `[]`) — keeps parsing simple

---

## data/sessions.jsonl

Append-only log of every completed session.

```json
{
  "ts": "2026-04-29T14:30:00Z",
  "session_id": "dfm-2026-04-29-01",
  "player": "Danny",
  "character": "Ryu",
  "path": "elite",
  "questions_answered": 20,
  "questions_correct": 16,
  "final_bank": 425000,
  "best_streak": 7,
  "lifelines_used": ["50-50", "phone-friend"],
  "bonus_stages_completed": 2,
  "upgrades_purchased": ["Extra Lifeline"],
  "outcome": "completed",
  "elapsed_minutes": 38
}
```

| Field | Type | Notes |
|---|---|---|
| `outcome` | enum | `completed` / `busted` / `quit` / `paused` |

---

## data/weak-spots.jsonl

Shared schema with `examiner` (cross-skill compose). Append-only.

```json
{
  "ts": "2026-04-29T14:35:00Z",
  "session_id": "dfm-2026-04-29-01",
  "skill_source": "dataflow-millionaire",
  "topic": "dataflow",
  "subconcept": "Tidy-vs-Archive",
  "miss_count_to_date": 3,
  "user_answer": "Archive comes before Tidy",
  "canonical_answer": "Tidy comes before Archive (clean before storing)",
  "miss_type": "wrong-order"
}
```

The `skill_source` field distinguishes millionaire-misses from examiner-misses for cross-skill audit.

---

## data/seen.jsonl

14-day repeat block — same schema as `examiner/data/seen.jsonl`.

```json
{
  "ts": "2026-04-29T14:30:00Z",
  "question_hash": "sha256:...",
  "stage": "T",
  "expires_at": "2026-05-13T14:30:00Z"
}
```

---

## Forward compatibility

v0.2 adds optional `data/title-progression.jsonl` (one row per title earned with date + cumulative earnings + sessions count) for retroactive milestone display. v0.1 derives this on-the-fly from `sessions.jsonl`.
