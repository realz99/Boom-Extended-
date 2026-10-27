# Boom-Extended-
improved Athenas Boom for rookies

## Boom° B33# — extended edition

Based on Boom° v2 by athenav135 (MPL 2.0). Same Fractal Model / Boom sequence and every v2 feature (panel C-labels Live / Confirmed with the ● dot, entry-TF lanes, chart-built POI zones, C3–C5 invalidation, now C3–C6), hardened, with trade management and actionable alerts.

**Script:** `Boom B33.pine` (Pine v6) · TradingView title **Boom° B33#** · build b24 · 100,125 / 100,256 compiled tokens

## Build b24 — calm palette

Neon replaced with calm AMOLED colours (every text colour still >= 4.5:1 on black): candles teal up / slate grey down (chart bar colours and HTF panels), signals teal bull / dusty rose bear (CISD, entry zones, table, SMT, FVG), sand for transition / early CISD / projections, sage for done / C3 / the ● dot, softer purple / copper / blue for the 4H–7H / 1D–1W SMT families and the PW / PM key levels.

## Build b23 — C5 / C6 tracking (HTF + LTF)

Ported from FM° MTF HTF (C5-C6 port). New input **Last** (C-label row, 4–6, default 6; 4 = the original model).
- **HTF / model:** a recorded setup carries C4 → C5 → C6. Each new HTF candle keeps the stage's zone and opens the next one (previous candle mid ↔ its open). A stage that trades beyond the previous candle's extreme goes **xC5 / xC6** and the setup stops there. IC-CISD runs through C5 / C6.
- **HTF panels:** C-labels C1 … C6 (the model panel keeps at least 6 candles). The C4 toggle is now **C4+** (C4–C6).
- **LTF chart:** C4 / C5 / C6 zones and labels per stage; the last stage shows xCn when it failed.
- **Sequence table:** the live candle counts C3 … C6, then WAIT C2; C3–C6 taking the C2 extreme → XC2.
- Room: the trade's EXIT / STOP branches share one ledger row + alert (same text); the model candle's close is computed once per bar.

## Build b22 — CISD grade (A / B / C)

Every CISD the table tracks (the C2's and each lane entry's) gets a grade, inspired by cephxs CISD [Ultimate +] — graded, never hidden:
- **F — fast:** the CISD came within 3 execution candles of the extreme (a slow CISD = a stale move).
- **S — sized:** its leg (CISD level to extreme) is at least 0.5 ATR of its own timeframe.
- **★ — origin:** the leg starts in an FVG.

A = all three, B = two, C = otherwise. Shown on the CISD row (e.g. `4011.5 A`), the lane entry rows, the SETUP / ENTRY alerts and the ledger.

## Build b21 — full parity with Boom° v2

Audited against the original v2 (every input, function, table row and alert). Nothing of v2 is dropped except what was removed on request (HTF Open, Vertical Lines, L/H Lines, Previous EQ, and the 90m / 6H / 12H / 1M / 3M / 12M SMT families). Restored in this build:
- The original dashboard's info, now in the table header: asset, alignment (chart TF / model TF) and date.
- The POI row shows which timeframes it searched when there is no POI (e.g. ✗ POI · 1H/4H/D).

## Build b20 — one CISD, one set of targets

- For the table's C2 the chart shows one CISD (the entry line) and one set of std-dev labels, drawn from the plan: 0 = entry, 1 = the C2 extreme (stop). The take-profits use the same formula, so TP1 / TP2 / TP3 sit exactly on the −1 / −2 / −4 labels (with the default TP std devs 1, 2, 4). Before, the chart's own CISD line and projections for that C2 used a different anchor and showed different prices.

## Build b19 — the standing C2 drives the plan

- While the latest confirmed C2 stands, its plan (E / SL / TPs) shows in the table and its entry line runs to price on the chart — from the moment it closes (C2 ✓) until it is invalidated or replaced. Before, on the C2 ✓ bar the chart could still extend the previous formation's CISD (e.g. a BUY CISD while the table showed a new bearish C2).

## Build b18 — one entry, trade direction fixed

- **Fixed a wrong-direction trade:** on the bar a new C2 confirmed, a lane entry from the previous C2 could open a trade carrying the new C2's opposite plan (e.g. ▲ IN with a bearish stop and targets). Lanes, trade, plan and alerts now act only when they refer to the same C2.
- **One entry price:** the table's E row and the chart line show the C2's CISD level until a lane fills, then the fill. EXEC shows the state only (▲ IN · TP1 …). Targets stay the C2 leg's projections; R is measured from the fill.

## Build b17 — FVGs by price proximity

- **MTF FVG boxes show the zones nearest to price**, on both sides, per timeframe (4H model, on any chart above 1m: 4H, 1H, Daily; 1H model, on a 1m chart: 1H, 15m, 4H, Daily). Price inside a zone shows it first. Before, the newest zones were shown, which could all be far from price.
- Same zones the C2 POI score reads; a zone leaves when a candle of its own timeframe wicks fully through it.

## Build b16 — FVG zones fixed, current CISD to price

- **MTF FVG boxes are back.** Fixed a bug in the original v2 zone builder (it compared a time with an empty value, which is never true in Pine, so no POI zone was ever built): MTF FVG boxes draw again, the POI row scores again, and ★ (leg from an FVG) and FVG-bounce alerts work again.
- **Current CISD runs to price:** the current formation's CISD line (the table's C2 while it stands, else the latest formation) extends to the live bar with your Buy / Sell text, whenever the table's entry line is not already showing. One extended line at a time.

## Build b15 — single source of truth

- **One entry everywhere:** E = the C2's CISD level in the table, on the chart line, in the SETUP alert, the ledger and the TP math. The lane fill shows on the EXEC row (`▼ IN 4011.6`). Prices keep 2 decimals, so table and chart read the same number.
- **An invalidated C2 stays dead:** once C3–C5 takes its protected extreme, its lanes, entries, trade, FVG bounce and plan rows stay off until the next C2 (before, they could re-open on the next candle when "C3 only" was off).
- **The table's C2 drives the chart:** its C2 tag shows the table's own score; "Latest Formation Only" highlights the table's C2 while it stands; the panel's Confirmed C2 is the same candle.
- **One gate for the lanes:** table lane rows, lane alerts, ledger and trade all use the same rule (C3-only option, bias filter). EXEC shows BIAS FILTER when the bias filter blocks the side.

## Build b14

- **Rebased on the author's Boom° v2.** Every v2 change is in: panel C-Labels Live / Confirmed with the ● dot on a C2 the table confirmed, lanes fed from their entry-TF candles (no 1m data needed; `--` when a step has no data), POI zones built from the chart's bars, C3–C5 that takes a confirmed C2's extreme invalidates it.
- **Panel C-Labels default to Confirmed** (the CISD gate): panel, table and chart entry show the same C2.
- **Key levels back:** Day Open (Midnight TDO / 6 PM D OPEN), PDH / PDL, PWH / PWL, PMH / PML + EQ — the original's levels and settings, neon defaults.
- **SMT families trimmed** to 15m, 30m, 1H, 4H, 7H, 1D, 1W (90m / 6H / 12H / 1M / 3M / 12M removed).
- **Trade gate = table gate:** no trade opens on an invalidated C2.
- Code reuse (one call site per repeated calculation) keeps every feature under TradingView's size limit.

## What is new vs the original

### Fractal Model logic
- CISD gate (the author's own fix): a C2 setup and its CISD line only show once the CISD confirms — in C2, C3 or C4. A C2 that never gets a CISD is never drawn.
- The CISD may now confirm in C4 (the original dropped setups at C4 open).
- Panel C-Labels default to Confirmed: the model panel labels the C2 the table confirmed (with its CISD), so the panel, the table and the chart entry show the same C2.
- Engine rebuilt as one code path for both sides: the first bar of C3 is no longer counted as part of C2; the C2 label sits on the C2 extreme; a C2 extreme taken in C4 starts the next C2 against C3; C4 invalidation also covers C4-confirmed setups; the setup history cap always applies.

### Sequence table (same information as the original, plus more)
- Narrow 2-column layout; text contrast computed in code (WCAG AA), whatever colours you pick.
- Added rows: SMT pairs in use, ATR trend + last flip, the entry price on the CISD row, Entry / Stop (break-even after TP1) and TP1 / TP2 that fill when hit, IN TRADE state.
- ★ marks a leg that starts in an FVG (C2 extreme or lane sweep traded into a POI FVG; adjustable touch %).

### Chart
- The table's entry is drawn on the chart: the BUY / SELL CISD line at the sequence C2's CISD level, running to price while the setup is tradeable (C3 / C4). Custom text.
- C2 label shows its confluence: C2+PSP+SMT+FVG.
- MTF FVG boxes: the exact POI zones the score uses (1H model: 1H / 15m / 4H / D; 4H model: 4H / 1H / D).
- Candle colours from an ATR trend channel (adapted from "ATR Trend Channel Signals" © BigBeluga, CC BY-NC-SA 4.0).
- Label backing for readability; AMOLED-black bright-neon palette, all text ≥ 4.5:1 contrast.

### Trade management
- A trade opens on the first lane entry (same gate as the table: never on an invalidated C2). Targets = std-dev projections of the C2 leg (Entry + n × |Entry − C2 extreme|, default 1, 2, 4). Stop = the C2 extreme, moved to break-even after TP1.
- Tracks TP1–TP3, stop, break-even stop and exit (a new C2), each with the result in R.

### Ledger
- The last 18 events as a glyph grid (▲ bull / ▼ bear, coloured by event) plus the newest event spelled out. Hover any glyph for price, time and details. Live vs history shading.
- Events: C2 setup, lane sweep, entry, FVG bounce, TP1–3, break-even, stop, exit, XC2, IC-CISD.

### Actionable alerts (one TradingView alert: "Any alert() function call")
- One alert per event, action first: BUY / SELL SETUP (limit at the CISD line) · ARMED (lane sweep) · BUY / SELL NOW (entry) · WATCH (FVG bounce) · TAKE TP1–3 · STOPPED / STOPPED AT BREAK-EVEN · CLOSE NOW.
- Each carries price, stop, TP1–3 and RR1 where they apply, plus the confluence (FVG zone, SMT, SMT-Fill, PSP).
- Every event is sent once — no repeats on live ticks.
- Text or JSON format. JSON (webhook / execution bridge): event, side, symbol, tf, price, sl, tp1, tp2, tp3, rr1, id, info — the id links a setup's entry, targets and exit.

### SMT
- One SMT settings section (pairs first, then panel SMT / PSP, labels, styling, gates; then families, then SMT-Fill).
- Families: 15m, 30m, 1H, 4H, 7H, 1D, 1W (the timeframes the model trades; 90m / 6H / 12H / 1M / 3M / 12M removed).
- Gold: four configurable correlated assets (default XAGUSD, XPTUSD, COPPER, TVC:DXY with an inverse switch); the first two ticked are the SMT pairs.

### FVG
- One FVG rule for every FVG in the script (POI zones, MTF boxes, HTF panel FVGs).
- POI (original score): the nearest same-side FVG in the C1–C2 range on the POI timeframes; the table names it (e.g. 1H BISI★, +F = SMT-Fill too).
- MTF FVG boxes on the chart are those exact POI zones.
- Near-touch: a C2 extreme inside the zone or within "POI touch %" of C1's range counts, so the C2 label shows +FVG when price almost tagged it. ★ = the leg starts in the FVG.
- FVG bounce: from C3 on, a wick into the bias-side POI zone that closes back out → ledger event + WATCH alert.

### Key levels
- The original's Day Open (Midnight TDO / 6 PM D OPEN), PDH / PDL, PWH / PWL, PMH / PML and their EQs: same levels, anchors, EQ rule and settings, computed by one tracker and drawn in one pass. AMOLED neon defaults (the original greys vanish on black).

### Other
- Removed on request: HTF Open, Vertical Lines, L/H Lines, Previous EQ. The dashboard box is folded into the table.
- Companion indicator FM° LIQ MAP adds sessions, BSL / SSL, EQH / EQL, first-presented FVG, IFVG and BPR.
- Code reuse: one call site per repeated calculation (SMT families, sources, pairs, bull / bear engine, key levels, table rows), so every feature fits within TradingView's size limit.

Libraries: GXVAssetCorrelationUtils, GXVUtils and QTSmtFillEngine by Gregorius_XV.
