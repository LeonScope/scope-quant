# Verification record

**20 October 2026 · local macOS application · engine 1.0.1 · synthetic data**

[Deutsch](#deutsch) · [Project](../README.md)

## Automated tests

**52 tests passed**, with resource warnings treated as errors. The tests ran against the private application. This repository does not publish the test source or a public CI workflow.

| Area | Evidence |
| --- | --- |
| Import | Explicit offsets, DST conversion, complete sessions, duplicates, chronological order, valid OHLC, finite tick-aligned prices and nonnegative integer volume |
| Data integrity | Original-byte preservation, independent canonical fingerprint, tampered staging/storage rejection and concurrent duplicate commits |
| Timing | No same-bar entry; changing future bars leaves earlier events and account states unchanged |
| Execution | Partial quantities, three-minute expiry, gap stops, entry gaps beyond target and conservative stop-before-target handling |
| Risk and accounting | Independent cash arithmetic, fees on both sides, one shared ledger, daily pauses, cash non-negativity and trade-PnL reconciliation |
| Research | Chronological split, selection rule, forward-only windows, equal baseline/stress input period and an actually reduced risk limit |
| Local model boundary | Existing distinct fact IDs, comparison-only difference facts, matching data versions and rejected model-digest changes |
| Persistence and reports | Restart behavior, interrupted jobs, saved runs, report cancellation, three-page PDFs, CSV values and unchanged earlier reports |
| Local HTTP surface | Host/Origin restrictions, mutation header, invalid input rejection, CSP and inaccessible source/database/model paths |

Two small arithmetic examples are independent of the demonstration dataset:

- Buying **99 units at 100.20** and selling at **100.30**, with zero modeled costs, produces **9.90** in net PnL.
- With the configured spread/slippage, the prices become **100.22 / 100.28**. Fees of **0.02 per unit per side** total **3.96**, leaving **1.98** net.

Another fixture touches both stop and target within one minute. The simulation takes the stop at **100.04**, resulting in **−15.84** for 99 units, and records the ambiguity.

## Browser and integration checks

The application was exercised using **48 synthetic sessions and 8,640 bars**. The baseline contains 82 closed trades and 215 partial-fill events. A separate run with a 0.12% daily threshold contains 65 closed trades, 169 partial-fill events, 19 daily pauses and 18 rejected entry signals. These are fixture outcomes, not market performance claims.

The observed browser flow included:

- Selecting a session, scrubbing, stepping and playing the stored replay.
- Continuing across a session boundary, then pausing.
- Opening a partial-fill event and inspecting its quantity, price and cash balance.
- Changing risk settings, calculating a separate run and comparing it with the baseline.
- Repeating a run and receiving the identical result fingerprint.
- Selecting an actual local CSV through the file chooser; validation and duplicate commit succeeded.
- Blocking a file containing an invalid negative price and an incomplete session.
- Running the research lab, observing the holdout result and the displayed stress assumptions.
- Generating and retrieving PDF/CSV reports.

The four work areas were checked at widths of **320, 390, 820 and 1440 pixels**, without page-level horizontal overflow. Wide tables scroll within their containers. The populated research table was also checked at 320 pixels. Resizing the risk pane was exercised with the keyboard. No console warnings or errors were observed in the checked session. These are desktop viewport checks, not physical-device or cross-browser certification.

Local Qwen3 4B inference was exercised for individual-run findings and a comparison. The final comparison selected calculated PnL and fee differences and proposed a cost-sensitivity test. Early development comparison drafts were tightened to require difference facts. All numeric sentences are rendered from application templates; this is a bounded prioritization workflow, not a general model reliability evaluation.

## Presentation artifacts

The screenshots and walkthrough were captured from the running local application. The recording follows replay, event inspection, a risk pause, the research lab, blocked import and the journal. Its setup hold was removed; captured action timing was retained.

The private report has **three pages**, all rendered and visually inspected. The public [two-page excerpt](../assets/report-excerpt.pdf) includes only the synthetic summary and assumptions. The detailed event page, source price series and trade CSV stay private. Downloaded report bytes were checked against stored SHA-256 values.

## What was not established

No actual exchange dataset, brokerage order, live market feed, production-scale load, multiuser deployment or real-market profitability was validated. Entry liquidity is approximated from whole-minute volume; exits are assumed to fill fully. Risk limits do not guarantee a maximum realized loss. A known holdout does not become unseen again when a new experiment is created.

---

## Deutsch

**20. Oktober 2026 · lokale macOS-Anwendung · Engine 1.0.1 · synthetische Daten**

**52 automatisierte Tests bestanden.** Ressourcenwarnungen wurden als Fehler behandelt. Die Tests liefen gegen die private Anwendung; Testquellcode und eine öffentliche CI-Pipeline sind nicht Bestandteil dieser Präsentation.

Geprüft wurden Datenimport und Integrität, Zeitzonen und Sommerzeit, Zeitreihenfolge, Kurs- und Volumenfehler, spätere Orderausführung, Teilausführungen, Kurssprünge, Stop-Ziel-Mehrdeutigkeit, gemeinsame Kontoführung, Tagespausen, die chronologische Forschungsauswahl, begrenzte Modellantworten, gespeicherte Berichte und lokale Zugriffsbeschränkungen.

Zwei unabhängig berechnete Beispiele:

- **99 Stück zu 100,20 kaufen und zu 100,30 verkaufen:** ohne Kosten **9,90** Nettoergebnis.
- Mit modellierten Ausführungskosten **100,22 / 100,28** und **0,02 Gebühr je Stück und Seite** ergeben sich **3,96 Gebühren** und **1,98 netto**.

Ein weiterer Fall berührt Stop und Ziel innerhalb derselben Minute. Der Stop zu **100,04** wird zuerst gewertet; bei 99 Stück ergibt das **−15,84**. Die Mehrdeutigkeit wird protokolliert.

### Bedienung und Modell

Im Browser wurden **48 erfundene Sitzungen mit 8.640 Minuten** verwendet. Der Ausgangslauf enthält 82 abgeschlossene Trades und 215 Teilausführungen. Der getrennte Versuch mit 0,12 % Tageslimit enthält 65 abgeschlossene Trades, 169 Teilausführungen, 19 Tagespausen und 18 abgelehnte Einstiegssignale. Diese Zahlen beschreiben das Demonstrationsmaterial.

Geprüft wurden Sitzungswechsel, Zeitregler, Einzelschritt, fortlaufende Wiedergabe über eine Sitzungsgrenze, Ereignisdetails, neue Risikoeinstellungen, Vergleich, identische Wiederholung und der Import einer tatsächlich ausgewählten lokalen CSV. Ein doppelter Import wurde erkannt; ein ungültiger Preis sperrte das Speichern. Forschungslabor und PDF-/CSV-Ausgabe wurden in der Oberfläche ausgeführt.

Die vier Arbeitsbereiche wurden bei **320, 390, 820 und 1440 Pixeln** Ansichtsbreite ohne seitlichen Seitenüberlauf geprüft. Breite Tabellen scrollen im eigenen Bereich. Die befüllte Forschungstabelle wurde zusätzlich bei 320 Pixeln kontrolliert. Die Breite des Risikobereichs ließ sich per Tastatur ändern. In der geprüften Sitzung wurden keine Konsolenwarnungen oder -fehler beobachtet.

Qwen3 4B lief lokal für einzelne Befunde und einen Vergleich. Der abschließende Vergleich verwendete berechnete Ergebnis- und Gebührendifferenzen und schlug einen Kostentest vor. Während der Entwicklung wurde die Antwortauswahl für Vergleiche auf tatsächliche Differenzbefunde eingeschränkt. Die Zahlen kommen aus Anwendungsvorlagen. Daraus folgt keine allgemeine Zuverlässigkeitsquote des Modells.

### Dateien und Grenzen

Die Screenshots und die kurze Aufnahme zeigen die laufende Anwendung. Aus der Aufnahme wurde der Vorlauf vor der ersten Bedienung entfernt; die zeitliche Abfolge der aufgezeichneten Aktionen blieb erhalten.

Alle **drei Seiten** des privaten Berichts wurden gerendert und visuell geprüft. Der öffentliche [zweiseitige Auszug](../assets/report-excerpt.pdf) zeigt nur synthetische Zusammenfassungen und Annahmen. Ereignisseite, rohe Kursdaten und Trade-CSV bleiben privat. Die abgerufenen Berichtsdaten stimmen mit den gespeicherten Prüfsummen überein.

Echte Börsendaten, Brokerorders, Live-Kurse, Produktivlast, Mehrbenutzerbetrieb und Rentabilität am Markt wurden nicht geprüft. Die Liquidität neuer Einstiege wird aus dem gesamten Minutenvolumen angenähert; Ausstiege werden vollständig ausgeführt. Risikolimits garantieren keinen maximalen Verlust. Ein bereits betrachteter Testzeitraum gilt bei Wiederholung als bekannt.
