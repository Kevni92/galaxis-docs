# Galaxis – Fachliche Dokumentation

Dieses Repository ist die verbindliche fachliche Quelle für das Spiel **Galaxis**.

Hier wird beschrieben, **wie das Spiel funktioniert**: Spielregeln, Entitäten, Befehle, Zustände, Wechselwirkungen und fachliche Anforderungen. Konkreter Client- oder Servercode gehört nicht in dieses Repository.

## Dokumentationsstatus

Die fachliche MVP-Dokumentation ist [vollständig geprüft und freigegeben](DOCUMENTATION-STATUS.md).

## Implementierungsroadmap

Die projektübergreifende, server-first ausgerichtete Umsetzung ist unter [`roadmap/`](roadmap/README.md) beschrieben.

- [A0 bis A12 – vollständige Implementierungsroadmap](roadmap/IMPLEMENTATION-ROADMAP.md)
- [A0 lokal mit Codex umsetzen](roadmap/CODEX-A0.md)

Die Roadmap verbindet die Milestones und Issues in `galaxis-docs`, `galaxis-server` und `galaxis-client`. Jede Alpha endet mit einem kleinen spielbaren vertikalen Schnitt.

## Balancing

Numerische Zielwerte, Formeln, Referenzszenarien und die Balancing-Roadmap liegen unter [`balancing/`](balancing/README.md). Die aktuelle Zahlenbasis ist **Baseline v0.1** und noch nicht durch vollständige Simulation oder Playtests validiert.

## Verbindliche Projektregeln

Diese Dokumente müssen von Agenten in allen Galaxis-Repositories gelesen und befolgt werden:

1. [Arbeitsregeln für KI-Agenten](AGENTS.md)
2. [Arbeitsworkflow](WORKFLOW.md) – vom Fachkonzept bis zum Merge
3. [Kommunikation einer Agenten-Session](AGENT-COMMUNICATION.md) – Aufgabenverständnis, Abschlussbericht und nächste Empfehlung
4. [Teststrategie](TESTING.md) – schnelle, risikobasierte Tests und CI-Stufen
5. [Quellcodedokumentation](SOURCE-CODE.md) – kurze Kommentare, Fachverweise und Modulnavigation

## Unverbindliche Ideen

Unter [`ideas/`](ideas/README.md) werden mögliche spätere Ansätze gesammelt. Diese Inhalte gehören ausdrücklich nicht zur fachlichen Dokumentation und dürfen Spielregeln, Planung oder Umsetzung nicht beeinflussen.

## Ziel der Dokumentation

Die Dokumentation soll:

- alle Spielmechaniken eindeutig und widerspruchsfrei beschreiben,
- als Grundlage für Issues in `galaxis-client` und `galaxis-server` dienen,
- von Menschen, Claude und Codex schnell verstanden werden,
- die spätere REST-Schnittstelle fachlich vorbereiten,
- Entscheidungen langfristig nachvollziehbar machen.
