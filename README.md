# Boom-Extended-
improved Athenas Boom for rookies 

Boom° — extended edition
Based on Boom° by athenav135 (MPL 2.0). Same Fractal Model / Boom sequence, hardened, with trade management and actionable alerts.

WHAT IS NEW VS THE ORIGINAL

Fractal Model logic
• CISD gate (the author's own fix): a C2 setup and its CISD line only show once the CISD confirms — in C2, C3 or C4. A C2 that never gets a CISD is never drawn.
• The CISD may now confirm in C4 (the original dropped setups at C4 open).
• HTF panel C1–C4 labels follow the confirmed formation, not candle shape alone.
• Engine rebuilt as one code path for both sides: the first bar of C3 is no longer counted as part of C2; the C2 label sits on the C2 extreme; a C2 extreme taken in C4 starts the next C2 against C3; C4 invalidation also covers C4-confirmed setups; the setup history cap always applies.

Sequence table (same information as the original, plus more)
• Narrow 2-column layout; text contrast computed in code (WCAG AA), whatever colours you pick.
• Added rows: SMT pairs in use, ATR trend + last flip, the entry price on the CISD row, Entry / Stop (break-even after TP1) and TP1 / TP2 that fill when hit, IN TRADE state.
• ★ marks a leg that starts in an FVG (C2 extreme or lane sweep traded into a POI FVG; adjustable touch %).

Chart
• The table's entry is drawn on the chart: the BUY / SELL CISD line at the sequence C2's CISD level, running to price while the setup is tradeable (C3 / C4). Custom text.
• C2 label shows its confluence: C2+PSP+SMT+FVG.
• MTF FVG boxes: the exact POI zones the score uses (1H model: 1H / 15m / 4H / D; 4H model: 4H / 1H / D).
• Candle colours from an ATR trend channel (adapted from "ATR Trend Channel Signals" © BigBeluga, CC BY-NC-SA 4.0).
• Label backing for readability; AMOLED-black bright-neon palette, all text ≥ 4.5:1 contrast.

Trade management
• A trade opens on the first lane entry. Targets = std-dev projections of the C2 leg (Entry + n × |Entry − C2 extreme|, default 1, 2, 4). Stop = the C2 extreme, moved to break-even after TP1.
• Tracks TP1–TP3, stop, break-even stop and exit (a new C2), each with the result in R.

Ledger
• The last 18 events as a glyph grid (▲ bull / ▼ bear, coloured by event) plus the newest event spelled out. Hover any glyph for price, time and details. Live vs history shading.
• Events: C2 setup, lane sweep, entry, FVG bounce, TP1–3, break-even, stop, exit, XC2, IC-CISD.

Actionable alerts (one TradingView alert: "Any alert() function call")
• One alert per event, action first: BUY / SELL SETUP (limit at the CISD line) · ARMED (lane sweep) · BUY / SELL NOW (entry) · WATCH (FVG bounce) · TAKE TP1–3 · STOPPED / STOPPED AT BREAK-EVEN · CLOSE NOW.
• Each carries price, stop, TP1–3 and RR1 where they apply, plus the confluence (FVG zone, SMT, SMT-Fill, PSP).
• Every event is sent once — no repeats on live ticks.
• Text or JSON format. JSON (webhook / execution bridge): event, side, symbol, tf, price, sl, tp1, tp2, tp3, rr1, id, info — the id links a setup's entry, targets and exit.

SMT
• One SMT settings section (pairs first, then panel SMT / PSP, labels, styling, gates; then families, then SMT-Fill).
• Gold: four configurable correlated assets (default XAGUSD, XPTUSD, COPPER, TVC:DXY with an inverse switch); the first two ticked are the SMT pairs.

Other
• One FVG rule shared by the POI zones and the HTF panel FVGs.
• Removed on request: HTF Open, Vertical Lines, L/H Lines, Previous EQ. The dashboard box is folded into the table.
• The PD / PW / PM levels, their EQs and the day open live in the companion indicator FM° LIQ MAP (with sessions, BSL / SSL, EQH / EQL, first-presented FVG, IFVG, BPR), so this script stays within TradingView's size limit.

Libraries: GXVAssetCorrelationUtils, GXVUtils and QTSmtFillEngine by Gregorius_XV.
