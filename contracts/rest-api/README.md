# Fachliche REST-Anforderungen

Dieser Bereich beschreibt den verbindlichen REST-Vertrag zwischen Server und Clients.

## Vertrag

- [Galaxis REST API v1](galaxis-rest-v1.md)
- [Maschinenlesbare OpenAPI-v1-Spezifikation für A0](galaxis-rest-v1.yaml)
- [Maschinenlesbare OpenAPI-v1-Spezifikation für A1](galaxis-rest-v1-a1.yaml)

Die beiden maschinenlesbaren Dateien bilden gemeinsam den Vertrag der API-Hauptversion `v1`. Client- und Serverwerkzeuge müssen beide Spezifikationen validieren beziehungsweise für die Typgenerierung zusammenführen. A1 wiederholt die A0-Authentifizierungsendpunkte nicht, verwendet aber dasselbe Bearer-Sicherheitsmodell und Fehlerformat.

## Grundsätze

- Der Server ist autoritativ.
- Antworten werden nach Kampagnenzugriff und Reichswissen gefiltert.
- Befehle sind idempotent und asynchron verfolgbar.
- Zustände sind versioniert und inkrementell per REST synchronisierbar.
- Die konkreten OpenAPI-Dateien werden aus dem fachlichen Vertrag abgeleitet.

Zurück zu den [fachlichen Verträgen](../README.md).
