# Balancing-Änderungs- und Freigabeworkflow

Status: Baseline v0.1

## Zweck

Dieser Workflow ergänzt den allgemeinen [`WORKFLOW.md`](../WORKFLOW.md) für numerische Werte, Formeln, Kataloge und Pacingziele.

## 1. Problem beschreiben

Jede Änderung beginnt mit einem beobachtbaren Problem, nicht mit einer isolierten Wunschzahl.

Ein Balancing-Issue nennt:

- betroffenen Fachbereich,
- beobachtetes Verhalten,
- betroffene Spielerentscheidung,
- Ausgangswert oder aktuelle Formel,
- Zielkorridor,
- betroffene Metriken,
- relevante Referenzszenarien,
- mögliche Nebenwirkungen.

Beispiel:

```text
Beobachtung:
Die erste Kolonie wird im Median nach 1,4 Tagen beauftragt.

Ziel:
Tag 3 bis 6 im Standardprofil.

Hypothese:
Die Startreserve und Kolonieschiffkosten erlauben Expansion ohne
Opportunitätskosten.
```

## 2. Ursache untersuchen

Vor der Wertänderung wird geprüft:

- Ist die fachliche Regel korrekt implementiert?
- Ist die Metrik korrekt berechnet?
- Verursacht ein anderer Parameter die Abweichung?
- Handelt es sich um ein Daten-, Formel-, AI- oder UI-Problem?
- Ist das Referenzszenario repräsentativ?
- Liegt ein Exploit oder eine unbeabsichtigte Wechselwirkung vor?

Ein Implementierungsfehler wird nicht durch einen kompensierenden Balancingwert kaschiert.

## 3. Änderungshypothese formulieren

Die Hypothese enthält:

- genau veränderte Parameter oder Formelbestandteile,
- erwartete Richtung und Größenordnung,
- erwartete Wirkung auf Hauptmetrik,
- erwartete Nebenwirkungen,
- bewusst unveränderte Bereiche.

Möglichst wird nur die kleinste zusammenhängende Parametergruppe verändert.

## 4. Vergleichsbasis sichern

Vor der Änderung werden gespeichert:

- Balancingversion,
- Commit,
- Szenarioversion,
- Seedliste,
- Strategie- und AI-Profile,
- Metrikbericht,
- bekannte Ausreißer.

Ohne reproduzierbare Ausgangsbasis kann eine Änderung nur als Entwurf, nicht als validiert gelten.

## 5. Werte ändern

Die Änderung erfolgt in den maschinenlesbaren Daten des Server-Repositories. Parallel werden aktualisiert:

- maßgebliches Dokument unter `balancing/`,
- Balancingversion,
- Changelog,
- bei Bedarf Formel- oder Einheitendokument,
- betroffene Fixtures und Tests.

Eine Wertänderung darf keine neue Fachregel einführen. Ist eine Fachregel nötig, wird zuerst der normale Docs-Workflow durchlaufen.

## 6. Schnelle Prüfungen

Jede Änderung benötigt mindestens:

- Datenschema- und Referenzvalidierung,
- Unit-Tests betroffener Formeln,
- Erhaltungs- und Grenzwerttests,
- deterministische Wiederholung,
- betroffene kleine Referenzszenarien.

Zielzeit für lokale schnelle Balancingtests: möglichst unter 30 Sekunden.

## 7. Szenariovergleich

Vorher und nachher werden mit identischen Seeds und Strategieprofilen verglichen.

Der Bericht enthält:

- Hauptmetrik vor und nach Änderung,
- Verteilung statt nur Mittelwert,
- Anteil außerhalb Zielkorridor,
- Nebenmetriken,
- unerwartete Veränderungen,
- Laufzahl und technische Laufzeit.

## 8. Strategiematrix prüfen

Eine Änderung wird mindestens gegen folgende Archetypen geprüft, soweit der Fachbereich betroffen ist:

- Expansion,
- Konsolidierung,
- Forschung,
- Handel,
- Diplomatie,
- Militär,
- konservative Überlebensstrategie.

Ein Fix für eine Strategie darf nicht unbemerkt eine andere vollständig entwerten.

## 9. Playtestbedarf bestimmen

Ein Playtest ist erforderlich, wenn die Änderung wesentlich beeinflusst:

- wahrgenommene Wartezeit,
- Informationslast,
- Frustration oder Kontrollverlust,
- Attraktivität einer Entscheidung,
- Verständlichkeit von Kosten und Folgen,
- subjektive Spannung eines Konflikts,
- Länge oder Dramaturgie einer Kampagnenphase.

Reine Erhaltungs- oder Rundungskorrekturen benötigen normalerweise keinen gesonderten Playtest.

## 10. Statusentscheidung

### Entwurf

- Hypothese vorhanden,
- aber noch keine belastbaren Vergleichsdaten.

### Baseline

- technisch gültig,
- Referenzszenarien laufen,
- keine rote Qualitätsverletzung,
- Startwert für weitere Arbeit.

### Validiert

- zentrale Metriken im Zielkorridor,
- ausreichende Szenario- und Seedabdeckung,
- Strategievielfalt geprüft,
- notwendige Playtests durchgeführt,
- bekannte gelbe Abweichungen besitzen Folge-Issues.

### Release

- Release-Szenariomatrix vollständig,
- keine roten Befunde,
- Savegame- und Kompatibilitätswirkung geprüft,
- Version eingefroren,
- Freigabe dokumentiert.

## 11. Pull-Request-Anforderungen

Eine Balancing-PR nennt:

- Issue und Balancingversion,
- fachliche Quelle,
- geänderte Parameter oder Formeln,
- Ausgangs- und Zielwerte,
- Hypothese,
- ausgeführte Tests und Szenarien,
- Vorher-/Nachher-Metriken,
- Savegame-Wirkung,
- bekannte Risiken,
- Rollback-Möglichkeit.

Große Sammeländerungen ohne getrennte Messbarkeit sind zu vermeiden.

## 12. Changelog

Jede freigegebene Änderung erhält einen Eintrag mit:

- Datum,
- Version,
- Status,
- Issue,
- geänderten Parametern,
- Begründung,
- Metrikergebnis,
- Kompatibilität.

## 13. Rollback

Eine Änderung muss zurücknehmbar sein, wenn:

- eine rote Qualitätsverletzung auftritt,
- Savegames beschädigt werden,
- eine dominante Strategie entsteht,
- zentrale Metriken deutlich außerhalb des Zielkorridors liegen,
- die Wirkung nicht reproduziert werden kann.

Rollback bedeutet eine neue nachvollziehbare Version; veröffentlichte Daten werden nicht stillschweigend überschrieben.

## 14. Umgang mit mehreren Änderungen

Mehrere Parameter dürfen gemeinsam geändert werden, wenn sie eine untrennbare Formel oder einen geschlossenen Regelkreis bilden. Der Bericht muss dann über Ablationsläufe oder begründete Teilvergleiche zeigen, welcher Bestandteil welche Wirkung besitzt.

## 15. AI- und LLM-Nutzung

AI darf:

- Ergebnisberichte zusammenfassen,
- Ausreißer gruppieren,
- Hypothesen und Folgefragen vorschlagen,
- Szenarien variieren,
- Daten auf Inkonsistenzen prüfen.

AI darf nicht allein entscheiden, dass eine Baseline validiert oder releasefähig ist. Maßgeblich bleiben reproduzierbare Simulationen, fachliche Invarianten und dokumentierte Playtests.