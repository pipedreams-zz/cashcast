# CashCast Lite — Liquiditätsplaner

Eine eigenständige, **lokale** Web-App zur Liquiditätsplanung: Startkontostand eingeben, geplante Einnahmen und Ausgaben (auch wiederkehrend) erfassen, und sofort den Kontostandsverlauf in die Zukunft sehen. Keine Cloud, kein Server, kein Login — alle Daten bleiben im Browser.

> Diese „Lite"-Insellösung ist der Prototyp für das Bedien- und Forecast-Konzept. Die spätere Vollversion (CashCast) soll als dünne Forecast-Schicht auf **Actual Budget** aufsetzen.

---

## Inhalt
- [Schnellstart](#schnellstart)
- [Benutzer-Anleitung](#benutzer-anleitung)
- [Technische Hinweise](#technische-hinweise)
- [Datenformat](#datenformat)

---

## Schnellstart

1. **`index.html` per Doppelklick öffnen** — läuft in jedem modernen Browser, komplett offline.
2. Beim ersten Start sind **Beispieldaten** geladen, damit du sofort siehst, wie alles wirkt.
3. Über **⋯ → Alles löschen** bekommst du eine leere Tafel für deine echten Zahlen.

> Tipp: Lege dir nach den ersten Eingaben über **⋯ → Exportieren** ein Backup an (eine JSON-Datei). Das ist gleichzeitig deine Sicherung und lässt sich jederzeit wieder importieren.

---

## Benutzer-Anleitung

### Grundprinzip
Du gibst einen **Startkontostand zu einem Stichtag** an. Von dort schreibt die App den Kontostand Tag für Tag fort, indem sie alle geplanten Zahlungen zum jeweils **exakten Datum** verrechnet. Das Ergebnis ist die **Liquiditätskurve**.

### Startkontostand
Button **„Startkontostand"** → Betrag und Stichtag setzen. Ab diesem Tag und Stand wird gerechnet.

### Zahlungen erfassen
Button **„+ Zahlung"**:
- **Einnahme / Ausgabe** umschalten (bestimmt das Vorzeichen).
- **Bezeichnung, Betrag, Datum.**
- **Kategorie** (siehe unten).
- **Szenario** — „Basis" für deinen festen Plan, oder ein Szenario (siehe unten).
- **Wiederholung** — einmalig, wöchentlich, monatlich, vierteljährlich, **halbjährlich** oder jährlich, optional mit Enddatum. Wiederholungen werden immer vom Originaldatum aus berechnet (kein Datums-Driften am Monatsende).

Eine Zahlung später bearbeiten: auf das **✎** in der Liste klicken.

### Liquiditätsverlauf (Chart)
- **Stufenkurve**: Der Kontostand springt am Buchungstag und ist dazwischen konstant — so verhält sich ein echtes Konto.
- **Heute-Markierung** und eine **rote Warnzone unter 0 €**.
- **Hover** über einen Punkt zeigt die Buchungen dieses Tages.
- Oben rechts der angezeigte **Zeitraum**.

### Kennzahlen (oben)
- **Stand heute** — Kontostand zum heutigen Tag.
- **Tiefststand** — der niedrigste Punkt im angezeigten Zeitraum samt Datum (die wichtigste Zahl für die Liquiditätsplanung). Wird er negativ, erscheint eine Warnung.
- **Ende Horizont** — Kontostand am Ende des gewählten Zeitraums.
- **Startkontostand** — dein Ausgangswert.

### Horizont
Auswahl oben (3 / 6 / 12 / 24 Monate): legt fest, wie weit Wiederholungen und Kurve in die Zukunft reichen.

### „Vergangenes" ein-/ausblenden
Standardmäßig beginnt die Ansicht **heute** und blickt nach vorn. Vergangene Zahlungen sind weiterhin **in der Berechnung** (der Kontostand heute ist also korrekt fortgeschrieben), werden aber erst angezeigt, wenn du **„Vergangenes"** aktivierst.

### Zahlungen abhaken (erledigt)
In der Liste sitzt vor jeder Zahlung ein **Häkchen-Kästchen**. Abhaken markiert die Zahlung als erledigt (Haken, durchgestrichen, ausgegraut). Das ist **rein optisch** — der Betrag bleibt voll in der Berechnung. Der Status wird **pro Termin** gespeichert, funktioniert also auch bei wiederkehrenden Zahlungen (Juli abgehakt ≠ August abgehakt).

### Kategorien
Jede Zahlung hat eine farbige Kategorie. Über **„Kategorien"** (Button oben) öffnet sich die Ansicht **„Ausgaben nach Kategorie"** und **„Einnahmen nach Kategorie"** — gestapelte Balken pro Monat in den Kategoriefarben.
- **Auf jedem Balken** steht die **Monats-Gesamtsumme** (bei bis zu 14 Monaten; bei längeren Horizonten ausgeblendet, um Überlappung zu vermeiden).
- **„Σ Horizont"** im Kopf jedes Diagramms = die **Gesamtsumme aller Ausgaben bzw. Einnahmen über den gesamten aktuell angezeigten Zeitraum** (von der Sichtgrenze — standardmäßig heute, mit „Vergangenes" ab Startdatum — bis zum Horizont-Ende). Sie ändert sich also mit Horizont und „Vergangenes".
- Kategorien anlegen/umbenennen/Farbe ändern/löschen: Link **„Verwalten"** in der Zahlungs-Maske oder **⋯ → Kategorien verwalten**. Beim Löschen werden betroffene Zahlungen automatisch der ersten verbleibenden Kategorie zugeordnet.

### Szenarien („Was wäre wenn?")
- Ordne eine Zahlung in der Maske einem **Szenario** statt „Basis" zu (z. B. „Großauftrag" oder „Läuft gut").
- Szenarien anlegen: Link **„Verwalten"** beim Szenario-Feld oder **⋯ → Szenarien verwalten** (Name + Farbe).
- Sobald Szenarien existieren, erscheint über dem Chart eine **Szenario-Leiste**. Ein Klick auf einen Szenario-Chip schaltet ihn ein und zeigt eine **gestrichelte Vergleichslinie** im Chart: *Basis + dieses Szenario*. Mehrere gleichzeitig möglich.
- **Wichtig zur Konsistenz:** Liste, Kennzahlen und Kategorie-Diagramme spiegeln immer den **festen Basis-Plan**. Szenario-Zahlungen erscheinen in der Liste als hypothetische Zeilen (Kontostand „–") und wirken ausschließlich als Chart-Vergleichslinie. So bleibt „real geplant" sauber von „was-wäre-wenn" getrennt.

### Hell / Dunkel
Das **☾/☀-Symbol** oben schaltet zwischen hellem und dunklem Design um. Die Wahl wird gemerkt; beim allerersten Start folgt sie deiner System-Einstellung.

### Wo liegen meine Daten? (Wichtig!)
Alle Eingaben werden **automatisch im Browser gespeichert** (`localStorage`) — du musst nichts „speichern". Konkret:

- **Bleiben erhalten:** beim Schließen des Browsers, beim Neustart des Browsers und beim Neustart des Rechners.
- **Bleiben meist erhalten:** beim „Cache leeren", solange nur *zwischengespeicherte Bilder/Dateien* gelöscht werden.
- **Gehen verloren**, wenn du
  - beim Löschen ausdrücklich *„Cookies und andere Websitedaten"* mit auswählst,
  - im **privaten / Inkognito-Fenster** arbeitest, oder
  - einen **anderen Browser, ein anderes Profil oder einen anderen Rechner** verwendest.

Die Daten hängen an **diesem Browser auf diesem Gerät**. Zum Übertragen oder als echte Sicherung dient der Export.

### Backup: Daten sichern & übertragen (⋯-Menü)
- **Exportieren (JSON)** — speichert deinen kompletten Stand als Datei. Das ist dein **Backup** und zugleich der Weg, die Daten auf einen anderen Browser/Rechner zu übertragen.
- **Importieren (JSON)** — lädt eine solche Datei wieder ein. Ältere Exporte sind kompatibel (fehlende Felder werden automatisch ergänzt).
- **„Zuletzt gesichert: …"** — im ⋯-Menü siehst du, wann dein letztes Backup war.
- **Beispieldaten laden** / **Alles löschen.**

> **Empfehlung:** Exportiere ab und zu eine Backup-Datei und lege sie an einen sicheren Ort (z. B. Dokumente-/Cloud-Ordner). So bist du gegen versehentliches Löschen der Browserdaten abgesichert.

#### Automatische Backup-Erinnerung
Damit nichts verloren geht, ohne dass du daran denken musst:
- Die App fordert beim Start **persistenten Speicher** an (`navigator.storage.persist()`), damit der Browser die Daten nicht von selbst verdrängt.
- Sobald du eigene Daten erfasst hast und **noch kein Backup** existiert — oder das **letzte Backup älter als 14 Tage** ist — erscheint oben ein dezenter Hinweis-Balken mit **„Jetzt sichern"** (Ein-Klick-Export) und **„Später"**. Nach einem Export verschwindet er automatisch.

> **Grenze der Technik:** Eine reine Lokal-App kann ein bewusstes „alle Websitedaten löschen" nicht überleben — dann hilft nur eine zuvor exportierte Backup-Datei. Genau dafür ist die Erinnerung da.

### Datenschutz
Alles läuft **lokal im Browser** (Speicher: `localStorage`). Es gibt keinen Server, kein Konto und keine externen Aufrufe. Deine Finanzdaten verlassen deinen Rechner nicht. Ein Backup entsteht nur, wenn du selbst exportierst.

---

## Technische Hinweise

- **Eine einzige Datei** (`index.html`) — HTML, CSS und JavaScript ohne externe Bibliotheken oder CDN. Funktioniert offline.
- **Diagramme** sind handgezeichnetes SVG (keine Chart-Bibliothek).
- **Persistenz**: Browser-`localStorage`, Schlüssel `cashcast-lite-v1` (Daten) und `cashcast-lite-theme` (Hell/Dunkel). Daten gelten **pro Browser/Profil und pro Herkunft** (`file://` bzw. eine Server-Adresse) — zum Übertragen Export/Import nutzen.
- **Datumslogik**: ISO-Strings aus lokalen Datumsteilen (kein UTC), damit sich keine Tage verschieben. Wiederholungen werden vom Ankerdatum abgeleitet.

### Optional: lokale Vorschau über einen Server
Für Entwicklung/Tests liegt eine `.claude/launch.json` bei, die einen einfachen Python-Server startet:
```bash
python -m http.server 5500 --directory liquidity-lite
# danach: http://localhost:5500
```
Für die normale Nutzung **nicht nötig** — `index.html` einfach doppelklicken.

---

## Datenformat

Der Export ist eine JSON-Datei mit dieser Struktur:

```jsonc
{
  "startBalance": 4200,            // Startkontostand
  "startDate": "2026-06-11",       // Stichtag (YYYY-MM-DD)
  "horizon": 6,                    // Monate
  "group": "month",                // Listengruppierung: "month" | "week"
  "showCat": false,                // Kategorie-Diagramme sichtbar
  "showPast": false,               // Vergangenes anzeigen
  "cats": [                        // Kategorien
    { "id": "wohnen", "name": "Wohnen", "c": "#B0764F" }
  ],
  "scenarios": [                   // Szenarien
    { "id": "gross", "name": "Großauftrag", "c": "#6E8CA8", "active": true }
  ],
  "done": [ "e123|2026-07-01" ],   // erledigte Termine: "<entryId>|<datum>"
  "entries": [                     // Zahlungen
    {
      "id": "e123",
      "type": "expense",           // "income" | "expense"
      "desc": "Miete",
      "amount": 1200,              // immer positiv; Vorzeichen ergibt sich aus type
      "date": "2026-07-01",
      "cat": "wohnen",             // Kategorie-id
      "scenario": "base",          // "base" oder eine scenario-id
      "recur": "monthly",          // once | weekly | monthly | quarterly | halfyearly | yearly
      "until": null                // optionales Enddatum der Wiederholung (YYYY-MM-DD)
    }
  ]
}
```

---

*CashCast Lite — eigene Liquiditätskontrolle, lokal und privat.*
