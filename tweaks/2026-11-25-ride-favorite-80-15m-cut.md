# 2026-11-25 (12:55 PM PT) — cut the 15-minute favorite copy in SOL (fake money)

Routine tune-up. One variant disabled in this fleet (no new bets; open bets still settle; history kept in data/week2). Nothing else changed.

Run-to-date week-2 numbers at 12:45 PM PT (settled bets):
- ride_favorite_80_15m: 149 settled, 120 won, -$53.18 (-7%), and -$18.04 on 15 bets in the last 6 hours. Wins 81% but the expensive favorites don't pay enough to cover the losses.
- It was also removed from max_profit's 15-minute signal list (now down_ride_15m only).

Other 15-minute copies are small samples and stay on (BTC breakout_15m +$9.60 on 8; XRP model_lead_15m -$10.84 on 12, watching). Watching crowd (SOL -$65.95 on 184, ETH -$61.69 on 97, but BTC +$7.22 and it feeds max_profit). price_lag_5m/15m, ab_hedge_1h, auto_pick / bankroll_20 (originals only) and the $10 per-bet cap unchanged.

Deploy: push main, wait for the running slice's next state save, cancel it so the chain restarts on the new commit. Paper mode only; data/week1 untouched.
