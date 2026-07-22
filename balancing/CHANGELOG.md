# Balancing-Änderungsprotokoll

Dieses Protokoll enthält freigegebene Änderungen an Balancingzielen, Formeln und Datenständen.

## 0.1.0-baseline – 2026-07-22

Status: Baseline

### Neu

- eigener verbindlicher Balancingbereich unter `balancing/`,
- Quellenrang und Statusmodell,
- systemweite Pacing- und Stabilitätsziele,
- gemeinsame Einheiten, Modifikatorreihenfolge und Rundungsregeln,
- Messgrößen und Qualitätsampel,
- versioniertes maschinenlesbares Datenformat,
- Referenzszenarien für Start, Expansion, Mittellage, Krieg, Krise und Endgame,
- Fachbereichsbaselines für Kampagne, Kolonien, Bevölkerung, Wirtschaft, Forschung, Flotten, Diplomatie, Ereignisse und Endgame,
- Roadmap B1 bis B4,
- Änderungs- und Freigabeworkflow.

### Ziel

Eine vollständige erste Zahlen- und Messbasis für die MVP-Implementierung schaffen. Diese Version ist noch nicht durch umfangreiche Simulation oder Playtests validiert.

### Kompatibilität

- Gilt zunächst für neue Kampagnen und noch nicht implementierte Datenkataloge.
- Führt keine Änderung an den bereits freigegebenen Fachregeln ein.
- Produktive Serverdaten müssen diese Version später explizit referenzieren.

### Bekannte offene Punkte

- konkrete Güter-, Gebäude-, Technologie-, Schiffs- und Ereigniskataloge,
- exakte Kampagnenzeitfaktoren,
- empirische Kalibrierung der Zielkorridore,
- automatisierter Simulationsrunner,
- Savegame-Migrationen für spätere Wertänderungen.