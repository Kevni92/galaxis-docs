# Balancing-Datenformat

Status: Baseline v0.1

## Zweck

Produktive Werte sollen nicht über viele C++-Dateien verteilt oder unkommentiert hart codiert werden. Dieses Dokument definiert die fachlichen Mindestanforderungen an maschinenlesbare Balancingdaten.

Die konkrete technische Serialisierung kann JSON, YAML oder ein validiertes projektspezifisches Format sein. Für den MVP wird JSON als einfaches Austausch- und Testformat empfohlen.

## Trennung von Regeln und Daten

- Fachliche Zustände, Befehle und Invarianten bleiben in `docs/`, `contracts/` und Serverlogik.
- Numerische Parameter, Katalogwerte und Kurven liegen in versionierten Daten.
- Der Server lädt, validiert und verwendet die autoritative Version.
- Der Client erhält nur Werte, die für Darstellung, Erklärung oder Prognose benötigt werden.
- Der Client darf aus Balancingdaten keine eigene abweichende Simulation ableiten.

## Dateikopf

Jeder Datensatz besitzt mindestens:

```json
{
  "schema_version": "1.0",
  "balance_version": "0.1.0-baseline",
  "domain": "economy",
  "status": "baseline",
  "source": "balancing/domains/economy-and-supply.md",
  "effective_from": "new_campaigns",
  "parameters": {}
}
```

## Parameterstruktur

Ein Parameter soll maschinenlesbar und für Menschen nachvollziehbar sein:

```json
{
  "essential_reserve_target_days": {
    "value": 10,
    "unit": "campaign_days",
    "minimum": 0,
    "maximum": 60,
    "description": "Zielreserve für essentielle Güter eines stabilen Reiches",
    "source_section": "Wirtschaftliche Stabilität",
    "tags": ["economy", "supply", "pacing"]
  }
}
```

Nicht jeder Parameter benötigt zur Laufzeit Beschreibung und Tags. Der Build- oder Validierungsprozess muss jedoch eine Zuordnung zur Quelle erhalten können.

## Stabile Kennungen

Parameterkennungen:

- verwenden `snake_case`,
- bleiben über reine Wertänderungen stabil,
- werden bei Bedeutungsänderung nicht wiederverwendet,
- enthalten keine Einheit im Namen, wenn die Einheit separat definiert ist,
- sind innerhalb der Domäne eindeutig.

Eine Umbenennung oder Bedeutungsänderung benötigt Migration und Changelog-Eintrag.

## Einheiten

Erlaubte Einheiten werden zentral registriert, beispielsweise:

- `basis_points`,
- `ratio_1e4`,
- `campaign_seconds`,
- `campaign_hours`,
- `campaign_days`,
- `quantity_milliunits`,
- `population_units`,
- `currency_minor_units`,
- `research_points`,
- `distance_units`,
- `probability_ppm`.

Freie, nicht registrierte Einheitentexte dürfen die produktive Validierung nicht passieren.

## Wertearten

Unterstützte fachliche Arten:

- Skalar,
- ganzzahliger Bereich,
- Kurve mit Stützpunkten,
- Tabelle nach Stufe oder Kategorie,
- gewichtete Auswahl,
- Matrix, beispielsweise Wirksamkeit Schiffsklasse gegen Zielklasse,
- Formelparameter,
- Inhaltskatalog mit stabilen IDs.

Formeln selbst sollen möglichst im Code oder in einem ausdrücklich validierten Ausdrucksformat liegen. Unkontrolliert ausführbarer Skriptcode gehört nicht in Balancingdaten.

## Kurven

Beispiel für eine Sättigungskurve:

```json
{
  "administration_overload": {
    "type": "piecewise_linear",
    "input_unit": "capacity_ratio_basis_points",
    "output_unit": "efficiency_basis_points",
    "points": [
      { "x": 0, "y": 10000 },
      { "x": 10000, "y": 10000 },
      { "x": 12500, "y": 9000 },
      { "x": 15000, "y": 7500 },
      { "x": 20000, "y": 5000 }
    ],
    "outside_range": "clamp"
  }
}
```

Interpolation, Verhalten außerhalb des Bereichs und Rundung müssen eindeutig sein.

## Referenzen

Katalogeinträge referenzieren andere Einträge nur über stabile IDs. Der Validator prüft:

- Existenz des Ziels,
- erlaubte Referenzrichtung,
- keine verbotenen Zyklen,
- kompatible Einheiten und Kategorien,
- keine Referenz auf deaktivierte Einträge ohne Fallback.

## Versionierung

Empfohlenes Schema:

```text
MAJOR.MINOR.PATCH[-status]
```

- **MAJOR:** inkompatible Bedeutungs- oder Datenstrukturänderung,
- **MINOR:** neue Parameter oder größere abgestimmte Baselineänderung,
- **PATCH:** kompatible Wertkorrektur,
- Status beispielsweise `draft`, `baseline`, `validated`, `rc1` oder `release`.

## Kampagnen und Savegames

Jede Kampagne speichert mindestens:

- verwendete Balancingversion,
- verwendete Katalogversionen,
- Kampagnenzeitprofil,
- Seed und Generierungsparameter.

Eine laufende Kampagne darf nicht unbemerkt auf neue Werte wechseln.

Unterstützte Strategien:

1. Kampagne bleibt auf ihrer ursprünglichen Balancingversion.
2. Ausdrückliche Migration mit dokumentierten Regeln.
3. Neue Werte gelten nur für neu erzeugte Kampagnen.

Die gewählte Strategie wird pro Änderung dokumentiert.

## Validierung

Der Server oder ein separates Werkzeug muss vor Start mindestens prüfen:

- Schema und Pflichtfelder,
- eindeutige IDs,
- registrierte Einheiten,
- Wertebereiche,
- Referenzen,
- Kurvensortierung,
- Wahrscheinlichkeits- und Gewichtssummen,
- Überlaufgrenzen,
- verbotene negative Werte,
- bekannte Erhaltungskonflikte,
- erwartete Versionskompatibilität.

Fehlerhafte produktive Daten müssen den Start oder Build klar fehlschlagen lassen. Stilles Ersetzen durch Nullwerte ist nicht zulässig.

## Deterministischer Hash

Aus allen autoritativen Balancingdaten wird ein kanonischer Hash gebildet. Er dient:

- Replay- und Savegame-Prüfung,
- Simulationsvergleich,
- Fehlerberichten,
- Multiplayer-Kompatibilität,
- Nachweis, welche Werte tatsächlich verwendet wurden.

Reihenfolge, Whitespace oder Kommentare dürfen den fachlichen Hash nicht verändern, sofern das gewählte Format eine kanonische Darstellung unterstützt.

## Beispielhafte Verzeichnisstruktur im Server

```text
data/
  balancing/
    manifest.json
    campaign.json
    galaxy.json
    planets.json
    population.json
    economy.json
    research.json
    fleets.json
    diplomacy.json
    events.json
```

Diese Struktur ist eine Empfehlung und keine Verpflichtung für konkrete Modulnamen.

## Änderungen

Eine Datenänderung darf erst gemergt werden, wenn:

- das zugehörige Balancing-Issue verlinkt ist,
- Quelle und Version aktualisiert wurden,
- Validator und betroffene Tests erfolgreich sind,
- Referenzszenarien ausgeführt wurden,
- erwartete Savegame-Wirkung dokumentiert ist,
- `balancing/CHANGELOG.md` nachgeführt wurde.