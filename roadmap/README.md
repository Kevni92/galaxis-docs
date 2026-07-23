# Implementierungsroadmap

Dieser Bereich übersetzt die freigegebene fachliche Dokumentation in eine schrittweise, projektübergreifende Umsetzung für:

- `galaxis-docs`,
- `galaxis-server`,
- `galaxis-client`.

## Maßgebliche Dokumente

- [Server-first Implementierungsroadmap](IMPLEMENTATION-ROADMAP.md)
- [Decision 0007 – Client-UX, 3D-Raumdarstellung und Lokalisierung](../decisions/0007-client-ui-rendering-und-lokalisierung.md)
- [UI- und UX-Grundlage](../docs/12-ui-ux/README.md)
- [UI-Verträge](../contracts/ui/README.md)
- [A0 mit lokalem Codex umsetzen](CODEX-A0.md)

## Grundsatz

Die Umsetzung ist **server-first**, aber nicht clientlos. Jede Alpha endet mit einem kleinen bedienbaren vertikalen Schnitt und einer reproduzierbaren Abnahmedemo.

Ab A1 verwendet der Client eine gemeinsame Game Shell mit 3D-Sternensystem- und Galaxieansicht, autoritativer lokaler XY-Geometrie, Topbar, linkem Zugriffsmenü, rechtem Outliner sowie einheitlichen modalen Fenstern. Planet-, Stern-, Kolonie- und Flottendetails öffnen über der Raumansicht und ersetzen sie nicht durch eigene Vollbildseiten.

Die Roadmap ersetzt keine Fachregel. Bei Widersprüchen gelten weiterhin die Quellenprioritäten aus [`WORKFLOW.md`](../WORKFLOW.md). Alpha-Issues dürfen keine Spielregel erfinden, sondern müssen auf freigegebene Fach-, Vertrags-, Entscheidungs- und Balancingquellen verweisen.

## Prüfung vor Clientarbeit

Vor Beginn eines Client-Issues muss geprüft werden, ob dessen Text mit Decision 0007 und `docs/12-ui-ux/` übereinstimmt. Veraltete Vorgaben wie reine SVG-Systemkarten, ausschließlich zweidimensionale Galaxiekarten, fest vorgegebene lokale Navigationspunkte oder Vollbildseiten für Planetendetails müssen zuerst in der Planung korrigiert werden.

Der jeweilige Alpha-Slice implementiert nur die benötigten Komponenten und Befehle, aber kein abweichendes UX-Grundmodell.

## GitHub-Struktur

- Zentrales Roadmap-Issue: #114
- Alpha-Umbrellas: #115 bis #127
- konkrete Docs-Vertragsissues für A0 bis A3: #128 bis #131
- Server-Issues A0 bis A3: `Kevni92/galaxis-server#1` bis `#33`
- Client-Issues A0 bis A3: `Kevni92/galaxis-client#1` bis `#23`

GitHub Projects dürfen ergänzend als Ansicht verwendet werden. Issues, Milestones, Entscheidungen und diese Roadmap bleiben jedoch die verbindliche, von Agenten bearbeitbare Planung.
