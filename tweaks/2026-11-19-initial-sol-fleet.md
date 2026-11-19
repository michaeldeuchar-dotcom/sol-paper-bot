## 2026-11-19 — initial SOL fleet (fake money)
- Ported from the BTC paper bot. 8 variants: control, model_lead, ride_favorite_80, trend_volume, trend_down, breakdown, hourly_trend_down, hourly_trend.
- New in code: `min_lead_pct` gate, `sides` filter, per-variant `timeframe` (5m / 1h), price-scaled basis noise (0.04% of price, measured on 50 SOL 5m markets).
