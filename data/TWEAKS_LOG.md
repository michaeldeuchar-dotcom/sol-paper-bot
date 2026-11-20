
## 2026-11-19 — initial SOL fleet (fake money)
- Ported from the BTC paper bot. 8 variants: control, model_lead, ride_favorite_80, trend_volume, trend_down, breakdown, down_ride (5m), hourly_ride_down (1h). Hourly variants use the broader 4h downtrend only as a filter, per research (mid-hour 'already down' ride).
- New in code: `min_lead_pct` gate, `sides` filter, per-variant `timeframe` (5m / 1h), price-scaled basis noise (0.04% of price, measured on 50 SOL 5m markets).
- New `require_trend_sign` filter. Spreads: fills are always at the ask.

## 2026-11-19 (about 5:15 PM PT) — add `auto_pick` variant (fake money only)
- Why: the owner asked for a SOL bot that picks the best-performing strategy on its own instead of a fixed approach.
- What: new variant `auto_pick` (5m), its own separate fake account (`trades_auto_pick.csv`). The 8 existing variants are UNCHANGED and keep supplying the scores.
- Rules:
  - Each round it ranks the other 5-minute variants by net fake P&L on bets that settled in the last 6 hours; if nobody qualifies in that window it falls back to since-start.
  - A variant qualifies only with 5+ settled bets and positive P&L; if nobody qualifies, auto_pick sits out.
  - It follows the leader's bets (same side, same moment). If the leader isn't betting it follows the next-ranked qualifier, so it never takes both sides of one window.
  - First pick is taken at once; switching between two qualifiers needs the new one to be best at 2 straight round checks (no flapping). If the leader stops qualifying, it moves to the best qualifier at once.
  - Stake: flat $3 target including fee; when $3 can't buy Polymarket's 5-share minimum (asks of ~60c+) it rounds up to 5 shares, never above $5 total. Hard max $10 unchanged.
  - Every check and every leader switch is logged (`AUTO_PICK CHECK` / `AUTO_PICK SWITCH`) and each switch is appended to `data/week1/auto_pick_switches.csv`. The current pick is in `state.json` (`auto_pick`) and in `heartbeat.json`.
  - `hourly_ride_down` (1h) is not a candidate: auto_pick trades 5m windows only.
- Avoiding BTC `meta` flaws: flat stake (meta scaled stake up after hot streaks, so its biggest losses came right after a leader's best run); a switch needs confirmation; ptb is passed to the copied variant's rules so lead gates really apply (the SOL port of meta_decide forgot it).
- Also: `summarize.py` shows auto_pick's current pick and leaves it out of the "all variants together" total (it only copies others' bets); `scripts/ci_run.sh` saves `auto_pick_switches.csv`.
- Unchanged: end time Nov 23 11:30 AM PT, $10 hard max, no wallet, no real trades.

## 2026-11-19 (about 5:45 PM PT) — auto_pick follows ONLY its current pick (fake money only)
- Change: auto_pick no longer falls back to the next-ranked qualifying variant. If its current pick doesn't bet in a window, auto_pick sits out that window.
- Why: the fallback meant most of its bets copied lower-ranked variants (mostly `control`) instead of the pick it reports.
- Unchanged: 6h net-P&L ranking (since-start fallback), 5+ bets and positive P&L to qualify, two-check rule to switch leaders, flat $3 stake with round-up to the 5-share minimum capped at $5 total, $10 hard max, end time.
