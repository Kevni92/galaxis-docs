# Implementierungsroadmap

Dieser Bereich übersetzt die freigegebene fachliche Dokumentation in eine schrittweise, projektübergreifende Umsetzung für:

- `galaxis-docs`,
- `galaxis-server`,
- `galaxis-client`.

## Maßgebliche Dokumente

- [Server-first Implementierungsroadmap](IMPLEMENTATION-ROADMAP.md)
- [A0 mit lokalem Codex umsetzen](CODEX-A0.md)

## Grundsatz

Die Umsetzung ist **server-first**, aber nicht clientlos. Jede Alpha endet mit einem kleinen bedienbaren vertikalen Schnitt und einer reproduzierbaren Abnahmedemo.

Die Roadmap ersetzt keine Fachregel. Bei Widersprüchen gelten weiterhin die Quellenprioritäten aus [`WORKFLOW.md`](../WORKFLOW.md). Alpha-Issues dürfen keine Spielregel erfinden, sondern müssen auf freigegebene Fach-, Vertrags-, Entscheidungs- und Balancingquellen verweisen.

## GitHub-Struktur

- Zentrales Roadmap-Issue: #114
- Alpha-Umbrellas: #115 bis #127
- konkrete Docs-Vertragsissues für A0 bis A3: #128 bis #131
- Server-Issues A0 bis A3: `Kevni92/galaxis-server#1` bis `#33`
- Client-Issues A0 bis A3: `Kevni92/galaxis-client#1` bis `#23`

GitHub Projects dürfen ergänzend als Ansicht verwendet werden. Issues, Milestones und dieses Dokument bleiben jedoch die verbindliche, von Agenten bearbeitbare Planung.
