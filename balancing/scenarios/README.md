# Referenzszenarien

Status: Baseline v0.1

Referenzszenarien sind reproduzierbare Ausgangslagen für Balancing, Regression und Performance. Sie beschreiben keine zusätzliche Fachlogik, sondern kombinieren freigegebene Regeln und Baselinewerte zu prüfbaren Verläufen.

## Szenarien

- [S01 – Startreich und erster Check-in](s01-startreich.md)
- [S02 – Expansion gegen Konsolidierung](s02-expansion-vs-konsolidierung.md)
- [S03 – Mittleres Reich und Versorgungsnetz](s03-mittleres-reich.md)
- [S04 – Begrenzter Krieg und Wiederaufbau](s04-krieg-und-wiederaufbau.md)
- [S05 – Krise, Endgame und Abschluss](s05-krise-und-endgame.md)

## Stabile Szenariokennung

Format:

```text
BAL-S<NN>-<KURZNAME>-v<MAJOR>.<MINOR>
```

Beispiel:

```text
BAL-S01-STARTREICH-v1.0
```

Eine reine Textkorrektur ändert die Version nicht. Jede Änderung der Ausgangslage, erlaubten Strategie, Laufzeit oder Sollmetrik erhöht die Szenarioversion.

## Pflichtmetadaten

Jeder maschinenlesbare Lauf speichert:

- Szenario-ID und Version,
- Balancingversion und Hash,
- Build oder Commit,
- Seed,
- Zeitprofil,
- Controller- und Strategieprofile,
- Laufzeit in Kampagnenzeit,
- Start- und Endzustand,
- Ereignis- oder Befehlsprotokoll,
- Metrikbericht,
- Laufzeit und Ressourcenverbrauch der Simulation.

## Seedgruppen

Mindestens folgende Gruppen sollen verwendet werden:

- **Golden Seeds:** kleine feste Liste für schnelle Regression.
- **Coverage Seeds:** größere feste Liste für normale CI- oder Nachtläufe.
- **Exploration Seeds:** wechselnde Liste zur Suche nach neuen Ausreißern.
- **Reproduction Seeds:** Seeds aus gefundenen Fehlern oder ungewöhnlichen Kampagnen.

Ein Fehlerseed wird nicht entfernt, nur weil eine Änderung ihn repariert hat.

## Strategieprofile

Soweit anwendbar:

- ausgewogen,
- Expansion,
- Konsolidierung,
- Forschung,
- Handel,
- Diplomatie,
- Militär,
- konservatives Überleben,
- absichtlich fehlerhafte oder stressende Strategie.

Profile verwenden dieselben fachlichen Befehle wie Spieler. Sie dürfen keine versteckten Ressourcen, Informationen oder Sonderregeln erhalten.

## Laufarten

### Schnelllauf

- 1 bis 5 Seeds,
- wenige Strategieprofile,
- betroffene Teilmetriken,
- Zielzeit unter 30 Sekunden, sobald technisch möglich.

### PR-Lauf

- Golden Seeds,
- alle betroffenen Szenarien,
- zentrale Erhaltungs-, Determinismus- und Zielkorridorprüfungen,
- Zielzeit wenige Minuten.

### Nachtlauf

- Coverage Seeds,
- vollständige Strategiematrix,
- lange Kampagnen,
- Performance- und Ausreißerbericht.

### Release-Lauf

- Golden, Coverage und Reproduction Seeds,
- vollständige Szenariomatrix,
- Savegame-, Migrations- und Kompatibilitätsprüfung,
- eingefrorene Balancingversion.

## Ergebnisstatus

- **bestanden:** keine rote Verletzung; zentrale Ziele im Korridor,
- **bestanden mit Warnung:** gelbe Abweichung mit dokumentiertem Folge-Issue,
- **fehlgeschlagen:** rote Verletzung, nicht reproduzierbares Ergebnis oder fehlende Pflichtmetadaten.

## Vergleich

Vorher-/Nachher-Läufe verwenden identische:

- Szenarioversion,
- Seeds,
- Strategieprofile,
- Zeitprofile,
- Simulationsoptionen.

Ändert sich eine dieser Größen, muss der Bericht den Vergleich als eingeschränkt kennzeichnen.

## Ableitung in Code

Spätere ausführbare Fixtures sollen ihre Szenario-ID im Dateinamen und Testnamen tragen. Beispiel:

```text
tests/scenarios/BAL-S01-STARTREICH-v1.0.json
```

Die Dokumentdatei bleibt die verständliche Quelle für Zweck, Ziel und Interpretation; das Fixture ist die maschinenlesbare konkrete Ausgangslage.