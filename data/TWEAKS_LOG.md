
## 2026-11-19 — initial SOL fleet (fake money)
- Ported from the BTC paper bot. 8 variants: control, model_lead, ride_favorite_80, trend_volume, trend_down, breakdown, down_ride (5m), hourly_ride_down (1h). Hourly variants use the broader 4h downtrend only as a filter, per research (mid-hour 'already down' ride).
- New in code: `min_lead_pct` gate, `sides` filter, per-variant `timeframe` (5m / 1h), price-scaled basis noise (0.04% of price, measured on 50 SOL 5m markets).
- New `require_trend_sign` filter. Spreads: fills are always at the ask.
