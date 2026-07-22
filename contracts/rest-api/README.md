# Fachliche REST-Anforderungen

Dieser Bereich beschreibt den verbindlichen REST-Vertrag zwischen Server und Clients.

## Vertrag

- [Galaxis REST API v1](galaxis-rest-v1.md)
- [Maschinenlesbare OpenAPI-v1-Spezifikation](galaxis-rest-v1.yaml)

## Grundsätze

- Der Server ist autoritativ.
- Antworten werden nach Kampagnenzugriff und Reichswissen gefiltert.
- Befehle sind idempotent und asynchron verfolgbar.
- Zustände sind versioniert und inkrementell per REST synchronisierbar.
- Die konkrete OpenAPI-Datei wird aus diesem Vertrag abgeleitet.

Zurück zu den [fachlichen Verträgen](../README.md).
