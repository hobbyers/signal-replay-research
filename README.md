# Signal Replay — Claim vs Real Replay Market

Independent replay of published trading signals against public Binance USD-M
1-minute candles, across four windows: **1, 3, 7 and 30 days**.

All four windows are sliced from one point-in-time snapshot, so the numbers are
directly comparable. Every signal is graded against the provider's published
status and replayed under four stop-management models.

- `index.html` — overview, window comparison, method and limits
- `1d.html` `3d.html` `7d.html` `30d.html` — full ledger + five chart views per signal

## Headline (snapshot 2026-10-19 18:15 UTC)

| Window | Signals | Resolved | Claim net R | Hold-to-final |
| --- | --- | --- | --- | --- |
| 1 day | 35 | 10 | +29.24R | −10.00R |
| 3 days | 97 | 63 | +88.30R | −37.31R |
| 7 days | 251 | 198 | +216.32R | −115.76R |
| 30 days | 2362 | 2210 | +3243.62R | −770.68R |

## Read this first

- **Claim** is not a price record. It is the exit implied by the provider's
  published status. A status that says a target was *touched* does not mean the
  position was closed there, or that it stayed profitable afterwards.
- **Real Replay Market** re-reads the actual 1-minute path: entry fills only when
  price touches the published entry, the stop stays at stop1 unless a different
  model is chosen, and the trade ends at the stop or the final target.
- Intrabar order is unknown. When a candle touches both the stop and a target,
  the replay refuses to guess and marks the signal ambiguous.
- Delisted, renamed, or non-listed symbols are excluded from the replay side and
  shown honestly.
- Replayed R includes Binance USD-M fees (maker 0.02% on entry, taker 0.05% on
  exits); funding is not applied. **Claim R is a gross price ratio**, so on the
  same target it reads slightly higher (e.g. a full-target trade shows +4.03R
  gross versus +3.91R after fees).
- **Not trading advice.** A past touch is not evidence of a profitable trade.

## Local preview

Pages load their data with `fetch()`, so serve them over HTTP:

```bash
python3 -m http.server 8080
```
