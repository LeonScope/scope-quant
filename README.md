# Scope Quant

**English** · [Deutsch](README.de.md)

### See how each trade happened.

A backtest ends with a number. I wanted to be able to stop at any trade and see how it got there: the completed price bar, the strategy rule, the risk check and the order that followed.

Scope Quant is a working local application for that kind of investigation. It combines historical CSV imports, a market replay, two reference strategies, a shared simulated account and a research lab. Every saved run keeps its data version, settings and event history.

![Scope Quant research workstation with a market replay and decision log](assets/quant-workbench.jpg)

*The fictional QSIM instrument and all prices shown here are synthetic. These are screenshots of the running application; the results are not evidence of trading profitability.*

[Download the walkthrough (MP4)](assets/quant-walkthrough.mp4?raw=true) · [Read the verification record](docs/VERIFICATION.md) · [Open the two-page report excerpt](assets/report-excerpt.pdf)

## A trade you can inspect

The replay advances through completed minutes. Blue markers show entries; amber markers show exits. The event log stays in step with the chart, and each event opens its order reference, quantity, price and reason.

The Opening Range and SMA Trend reference strategies share one cash account. Pending entries can fill partially, expire or be rejected. A daily loss gate blocks further entries until the next session while existing protective orders remain active.

![Recorded operation of the private local application](assets/quant-preview.gif)

## Put the assumptions under pressure

The research lab compares six Opening Range variants on chronological development and validation periods, freezes the selection and evaluates the remaining holdout. Three rolling windows and cost-stress scenarios give the result more context. Reusing the holdout is explicitly identified as testing on familiar data.

![Chronological research windows and parameter comparison](assets/quant-research.jpg)

In the journal, two runs using the same dataset can be compared directly. A local Qwen3 4B model selects relevant calculated findings and suggests a follow-up test. The application supplies the numeric statements from checked templates; the model cannot change the simulation or submit orders.

## What I built

| Part | Working behavior |
| --- | --- |
| Data workshop | CSV inspection, session completeness, tick precision, duplicate protection and original-file fingerprints |
| Simulation | Completed-bar signals, next-minute entries, partial fills, cash accounting, fees, spread and slippage assumptions |
| Replay | Synchronized chart, positions and decision log; single-step, speed selection and continuous session playback |
| Risk | Shared capital, position limits, daily entry pause and visible rejection reasons |
| Research | Parameter comparison, chronological holdout, rolling windows, sensitivity tests and saved results |
| Journal | Same-data run comparison, bounded local model assistance, immutable PDF and CSV reports |

[Order details](assets/quant-event.jpg) · [Import validation](assets/quant-import.jpg) · [Research journal](assets/quant-journal.jpg) · [Mobile view](assets/quant-mobile.jpg)

The private application uses Python, SQLite, JavaScript, SVG charts, ReportLab and a local Ollama/Qwen3 runtime. I developed it with Codex and kept the design and verification focused on decisions that a reviewer can actually inspect. [Implementation choices and my role →](docs/CASE_STUDY.md)

## Scope of the simulation

This version models long-only, unleveraged cash positions in one instrument and currency. It uses complete one-minute OHLCV sessions. Whole-minute volume limits entry size as an approximation; protective exits are assumed to fill fully. If a candle touches both stop and target, the stop is processed first. Gaps and costs can exceed planned risk limits.

There is no broker connection, live market feed, order-book model, short selling, corporate-action adjustment or futures contract accounting. [Detailed assumptions →](docs/CASE_STUDY.md#execution-assumptions)

**Verified locally on 20 October 2026:** 52 automated tests passed, including independent cash calculations, prevention of same-bar entry, future-data isolation, gap handling, import integrity and report snapshots. The browser and local model were exercised with 48 synthetic sessions and 8,640 bars. [Checks and their limits →](docs/VERIFICATION.md)

**This repository contains the presentation only.** Source code, database, models, imported trading data, generated price series and trade CSV exports remain private. The report excerpt contains selected synthetic summary results and assumptions. No open-source license is granted for the original portfolio material. [Rights](RIGHTS.md) · [Third-party notices](THIRD_PARTY_NOTICES.md)
