# Third-party notices

The application screenshots and PDF excerpt use **IBM Plex Sans** and **IBM Plex Mono**, distributed under the SIL Open Font License. Their notices are included:

- [IBM Plex Sans notice](notices/PlexSans-OFL.txt)
- [IBM Plex Mono notice](notices/PlexMono-OFL.txt)

Official font sources were obtained from the [Google Fonts repository](https://github.com/google/fonts).

The private implementation uses Python, SQLite, ReportLab, Pillow, fontTools, pypdf, Ollama and Qwen3 4B. Source packages, runtimes and model weights are not redistributed here. Product names identify the tools used; no endorsement is implied.

The chart renderer and interface were implemented for this application. No third-party trading terminal screenshots, market feed or trading framework are included.

Technical background considered during design:

- [NautilusTrader concepts](https://nautilustrader.io/docs/latest/concepts/) — event, account and simulation boundaries.
- [QuantConnect trade fills](https://www.quantconnect.com/docs/v2/writing-algorithms/reality-modeling/trade-fills/key-concepts) — explicit assumptions about execution quantity and price.
- [QuantConnect walk-forward optimization](https://www.quantconnect.com/docs/v2/writing-algorithms/optimization/walk-forward-optimization) — chronological research windows.

These references informed the problem framing. Scope Quant is a separate, limited implementation.
