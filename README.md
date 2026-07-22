# Galaxis – Fachliche Dokumentation

Dieses Repository ist die verbindliche fachliche Quelle für das Spiel **Galaxis**.

Hier wird beschrieben, **wie das Spiel funktioniert**: Spielregeln, Entitäten, Befehle, Zustände, Wechselwirkungen und fachliche Anforderungen. Konkreter Client- oder Servercode gehört nicht in dieses Repository.

## Dokumentationsstatus

Die fachliche MVP-Dokumentation ist [vollständig geprüft und freigegeben](DOCUMENTATION-STATUS.md).

## Balancing

Numerische Zielwerte, Formeln, Referenzszenarien und die Balancing-Roadmap liegen unter [`balancing/`](balancing/README.md). Die aktuelle Zahlenbasis ist **Baseline v0.1** und noch nicht durch vollständige Simulation oder Playtests validiert.

## Verbindliche Projektregeln

Diese Dokumente müssen von Agenten in allen Galaxis-Repositories gelesen und befolgt werden:

1. [Arbeitsworkflow](WORKFLOW.md) – vom Fachkonzept bis zum Merge
2. [Teststrategie](TESTING.md) – schnelle, risikobasierte Tests und CI-Stufen
3. [Quellcodedokumentation](SOURCE-CODE.md) – kurze Kommentare, Fachverweise und Modulnavigation
4. [Arbeitsregeln für KI-Agenten](AGENTS.md)

## Unverbindliche Ideen

Unter [`ideas/`](ideas/README.md) werden mögliche spätere Ansätze gesammelt. Diese Inhalte gehören ausdrücklich nicht zur fachlichen Dokumentation und dürfen Spielregeln, Planung oder Umsetzung nicht beeinflussen.

## Ziel der Dokumentation

Die Dokumentation soll:

- alle Spielmechaniken eindeutig und widerspruchsfrei beschreiben,
- als Grundlage für Issues in `galaxis-client` und `galaxis-server` dienen,
- von Menschen, Claude und Codex schnell verstanden werden,
- die spätere REST-Schnittstelle fachlich vorbereiten,
- Entscheidungen langfristig nachvollziehbar machen.