# Balancing-Roadmap

Status: Baseline v0.1

## Ziel

Die Balancingarbeit wird in vier aufeinander aufbauende Milestones gegliedert. Jede Phase besitzt ein anderes Beweisniveau. Frühe Baselines müssen spielbar und messbar sein; Releasewerte benötigen deutlich breitere Simulation und Playtests.

## B1 – MVP-Baseline-Balancing

### Ziel

Eine vollständige erste Zahlenbasis herstellen, mit der alle freigegebenen MVP-Systeme implementiert, gestartet und in Referenzszenarien geprüft werden können.

### Ergebnisse

- systemweite Pacingziele,
- initiale Formeln und Einheiten,
- Startwerte für alle Fachbereiche,
- maschinenlesbares Datenformat,
- Validator,
- deterministische Referenzfixtures,
- erste Änderungs- und Versionsregeln.

### Freigabekriterium

- Alle MVP-Systeme besitzen Werte oder explizite ableitbare Defaults.
- Keine rote Qualitätsverletzung.
- Frühes, mittleres und spätes Referenzszenario laufen vollständig.
- Kampagnenverlauf ist grundsätzlich möglich, auch wenn Feinabstimmung noch fehlt.

## B2 – Automatisierte Simulationsprüfung

### Ziel

Balancingänderungen reproduzierbar über viele Seeds, AI-Profile und Szenarien vergleichen.

### Ergebnisse

- Headless-Simulationsrunner,
- standardisiertes Ergebnisformat,
- Metrikaggregation,
- Strategie- und AI-Archetypen,
- Regression-Schwellen,
- Nachtlauf und Berichte,
- Performance- und Langzeitmessung.

### Freigabekriterium

- Baselines sind mit identischen Seeds reproduzierbar.
- Vorher-/Nachher-Berichte werden automatisiert erzeugt.
- zentrale Qualitätsgrenzen können CI-seitig bewertet werden.
- Simulation und Offline-Nachholung liefern fachlich gleichwertige Ergebnisse.

## B3 – Playtest-Balancing

### Ziel

Subjektive Spielqualität, Verständlichkeit, Informationslast, Wartegefühl und strategische Attraktivität mit echten Spielsitzungen prüfen.

### Ergebnisse

- Playtestplan und Fragebogen,
- definierte Testgruppen und Szenarien,
- datensparsame Telemetrie oder manuelle Erfassung,
- Auswertung für frühes, mittleres und spätes Spiel,
- Prüfung von Gelegenheitsspiel und Intensivspiel,
- Nachweis strategischer Vielfalt.

### Freigabekriterium

- kritische Abläufe sind verständlich,
- täglicher Check-in funktioniert praktisch,
- kein wiederkehrender Frusttreiber bleibt ohne Folgeplan,
- wichtige Strategien werden als unterschiedlich und sinnvoll erlebt,
- Informationsmenge und Reaktionsfenster sind tragfähig.

## B4 – Release-Balancing

### Ziel

Eine konkrete Balancingversion für den ersten Release-Kandidaten stabilisieren und einfrieren.

### Ergebnisse

- vollständige Release-Szenariomatrix,
- validierte Kataloge und Werte,
- Savegame- und Migrationsregeln,
- finale Strategie- und Exploitprüfung,
- Performanceprüfung großer Kampagnen,
- Release-Changelog,
- eingefrorene Balancingversion.

### Freigabekriterium

- keine roten Befunde,
- alle gelben Befunde dokumentiert und akzeptiert,
- Releasewerte sind versioniert und unveränderlich referenzierbar,
- Kompatibilität und Rollback sind geklärt,
- Kampagnenbogen erreicht in Simulation und Playtest den vorgesehenen Bereich.

## Abhängigkeiten

```text
B1 Baseline
  ↓
B2 automatisierte Simulation
  ↓
B3 Playtests
  ↓
B4 Release-Freigabe
```

Einzelne Werkzeuge aus B2 dürfen bereits während B1 entstehen. B3 darf mit frühen Prototypen beginnen. Eine Phase gilt aber erst abgeschlossen, wenn ihre eigenen Freigabekriterien erfüllt sind.

## Nicht-Ziele

Die Roadmap verlangt nicht:

- perfekte Symmetrie aller Reiche,
- identische Erfolgschance jeder Strategie in jeder Lage,
- vollständige Vorhersagbarkeit,
- unveränderliche Werte nach Release,
- Telemetrie ohne ausdrückliche Datenschutz- und Produktentscheidung.

## Statusführung

Der aktuelle Status jedes Milestones wird in GitHub gepflegt. Dokumente unter `balancing/` nennen zusätzlich ihre eigene Version und Freigabestufe. Ein geschlossener Milestone ersetzt nicht die Versionsangabe der Daten.