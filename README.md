# CashCast

Eigene **Liquiditätsplanung** mit Zukunfts-Forecast — self-hosted, privacy-first.

Aktueller Bestandteil:

| Ordner | Inhalt |
|---|---|
| [`liquidity-lite/`](liquidity-lite/) | **CashCast Lite** — eigenständiger Prototyp: eine einzige HTML-Datei, ohne Server/Login, Daten lokal im Browser. Erprobt Bedien- und Forecast-Konzept. Siehe [liquidity-lite/README.md](liquidity-lite/README.md). |

Die **Vollversion** (geplant als dünne Forecast-Schicht auf **Actual Budget**) ist erst in Vorbereitung und noch nicht Teil dieses Repos.

## Stand

- ✅ **Lite-Prototyp** lauffähig (Forecast-Kurve, Kategorien, Szenarien, Wiederholungen, Erledigt-Status, Hell/Dunkel, JSON-Export/Import, Backup-Erinnerung).
- ⏳ **Vollversion**: erst geplant. Voraussetzung ist, dass die Kategorisierung in Actual (actual-ai) sauber genug ist — vorher validieren.

## Schnellstart (Lite)

`liquidity-lite/index.html` per Doppelklick im Browser öffnen. Alles Weitere im [Lite-README](liquidity-lite/README.md).

## Struktur

Monorepo: Der Lite-Prototyp liegt in `liquidity-lite/`. Die Vollversion kommt später als eigener Top-Level-Ordner (z. B. `web/`) hinzu.
