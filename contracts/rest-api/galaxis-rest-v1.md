# Galaxis REST API v1 – Fachlicher Vertrag

Status: Freigegeben

## Zweck

Dieser Vertrag definiert die implementierungsunabhängigen Anforderungen an die REST-Schnittstelle zwischen Galaxis-Server und Clients. Der Server bleibt für Spielzustand, Zeit, Wissen, Berechtigungen und Befehlsausführung autoritativ.

## Grundprinzipien

- Basispräfix: `/api/v1`.
- Transport über HTTPS außerhalb lokaler Entwicklung.
- Datenformat: UTF-8 JSON.
- Ressourcen verwenden stabile, undurchsichtige IDs.
- Zeitpunkte werden als ISO-8601 in UTC übertragen.
- Dauern werden als eindeutig benannte Kampagnenzeitwerte übertragen.
- Der Client darf keine lokale Zustandsänderung als bestätigt behandeln, bevor der Server sie angenommen hat.
- Jede Antwort ist nach Identität, Kampagnenzugriff, kontrolliertem Reich und dessen Wissen gefiltert.
- Spieler- und AI-Controller verwenden fachlich dieselben Befehlsressourcen.

## Versionierung

Die Hauptversion ist Bestandteil des Pfads. Innerhalb von v1 dürfen additive Felder ergänzt werden. Clients müssen unbekannte Felder ignorieren.

Entfernen, Umbenennen oder Bedeutungsänderungen bestehender Pflichtfelder benötigen eine neue Hauptversion oder eine ausdrücklich dokumentierte Übergangsphase.

Jede Antwort kann enthalten:

```json
{
  "apiVersion": "1.0",
  "schemaVersion": 1
}
```

## Authentifizierung

Geschützte Anfragen verwenden ein Bearer-Token. Das Token identifiziert einen Account oder internen Dienst, nicht automatisch ein Reich.

Mindestoperationen:

```text
POST   /api/v1/auth/sessions
DELETE /api/v1/auth/sessions/current
GET    /api/v1/auth/session
```

Die konkrete Anmeldemethode kann lokal, extern oder später austauschbar sein. Der REST-Vertrag benötigt nur eine bestätigte Sessionidentität.

## Kampagnenzugriff

Ein Account darf Kampagnen nur sehen, wenn er Teilnehmer, Besitzer, Beobachter oder ausdrücklich berechtigter Administrator ist.

```text
GET  /api/v1/campaigns
POST /api/v1/campaigns
GET  /api/v1/campaigns/{campaignId}
POST /api/v1/campaigns/{campaignId}/pause
POST /api/v1/campaigns/{campaignId}/resume
```

Pause und Fortsetzung sind Befehle und werden nur angeboten, wenn der Kampagnentyp und Account dies erlauben.

## Reichskontext

Ein Benutzer kann je Kampagne höchstens die ausdrücklich zugeordneten Reiche steuern. Lesen und Befehlen sind getrennte Berechtigungen.

```text
GET  /api/v1/campaigns/{campaignId}/empires
GET  /api/v1/campaigns/{campaignId}/empires/{empireId}
POST /api/v1/campaigns/{campaignId}/empires/{empireId}/takeover
POST /api/v1/campaigns/{campaignId}/empires/{empireId}/handover
GET  /api/v1/campaigns/{campaignId}/empires/{empireId}/takeover-report
```

Jede Befehlsanfrage prüft die Controllerzuordnung zum autoritativen Annahmezeitpunkt erneut.

## Ressourcenmodell

Die Schnittstelle stellt fachliche Ressourcen bereit, keine internen Klassen oder Datenbanktabellen.

Hauptressourcen:

- Kampagnen,
- Reiche,
- Galaxie und bekannte Sternensysteme,
- Himmelskörper,
- Kolonien und Bauaufträge,
- Bevölkerung und Beschäftigung,
- Bestände, Produktion, Transporte und Haushalt,
- Forschung und Technologien,
- Schiffe, Flotten, Reisen und Kämpfe,
- Beziehungen, Angebote, Verträge und Kriege,
- Ereignisse, Anomalien, Krisen und Entscheidungen,
- Befehle,
- Rückkehr- und Abschlussberichte.

Unterressourcen werden nach ihrem fachlichen Besitzer oder Kontext adressiert. Sehr große Sammlungen müssen paginierbar sein.

## Zustandsabfragen

### Kampagnenübersicht

```text
GET /api/v1/campaigns/{campaignId}/state
```

Liefert einen kompakten Einstieg:

- Kampagnenzeit und Laufzustand,
- kontrolliertes Reich,
- aktuelle Zustandsversion,
- wichtigste Warnungen,
- offene Entscheidungen,
- laufende Befehle,
- Linkrelationen zu Detailressourcen.

### Galaxie und Systeme

```text
GET /api/v1/campaigns/{campaignId}/galaxy
GET /api/v1/campaigns/{campaignId}/systems/{systemId}
```

Die Antwort enthält ausschließlich bekannte Systeme, Verbindungen und Eigenschaften. Unbekannte IDs, Objektzahlen und verborgene Felder werden nicht übertragen.

### Reichsbereiche

```text
GET /api/v1/campaigns/{campaignId}/empires/{empireId}/colonies
GET /api/v1/campaigns/{campaignId}/empires/{empireId}/population
GET /api/v1/campaigns/{campaignId}/empires/{empireId}/economy
GET /api/v1/campaigns/{campaignId}/empires/{empireId}/research
GET /api/v1/campaigns/{campaignId}/empires/{empireId}/fleets
GET /api/v1/campaigns/{campaignId}/empires/{empireId}/diplomacy
GET /api/v1/campaigns/{campaignId}/empires/{empireId}/events
```

Jede Übersicht bietet entscheidungsrelevante Zusammenfassungen und Links zu Detailressourcen.

## Zustandsversion

Jede autoritative Kampagne besitzt eine monoton steigende `stateVersion`. Zustandsänderungen erhöhen die Version atomar.

Antworten enthalten:

```json
{
  "campaignId": "cmp_...",
  "stateVersion": 1842,
  "generatedAt": "2026-07-22T12:00:00Z"
}
```

Die Version ist keine Kampagnenzeit und darf nicht zur fachlichen Dauerberechnung verwendet werden.

## Bedingte Abfragen und Caching

GET-Antworten können `ETag` enthalten. Clients senden `If-None-Match`; bei unverändertem sichtbarem Zustand antwortet der Server mit `304 Not Modified`.

Private, reichsspezifische Antworten dürfen nicht durch gemeinsam genutzte Caches zwischen Benutzern vermischt werden. Der Server setzt geeignete Cache-Header.

## Inkrementelle Aktualisierung

Der Client kann Änderungen seit einer bekannten Version abfragen:

```text
GET /api/v1/campaigns/{campaignId}/changes?after=1842&limit=200
```

Antwort:

```json
{
  "fromVersion": 1842,
  "toVersion": 1850,
  "hasMore": false,
  "changes": [
    {
      "version": 1845,
      "type": "colony.updated",
      "resource": "/api/v1/campaigns/cmp_1/colonies/col_7"
    }
  ]
}
```

Änderungen enthalten nur für den aktuellen Reichskontext sichtbare Informationen. Wird eine Version nicht mehr vorgehalten, antwortet der Server mit einem Fehler, der einen vollständigen Snapshot verlangt.

Optional darf der Server Long Polling unterstützen:

```text
GET /changes?after=1850&waitSeconds=20
```

Dies bleibt eine zustandslose HTTP-Abfrage und ist keine Voraussetzung für WebSockets.

## Befehlsübermittlung

Fachliche Änderungen werden über Befehlsressourcen eingereicht:

```text
POST /api/v1/campaigns/{campaignId}/commands
```

Beispiel:

```json
{
  "clientCommandId": "01J...",
  "empireId": "emp_1",
  "type": "fleet.move",
  "expectedStateVersion": 1842,
  "payload": {
    "fleetId": "flt_9",
    "targetSystemId": "sys_12",
    "route": ["con_4", "con_8"]
  }
}
```

`clientCommandId` ist innerhalb von Account und Kampagne eindeutig und dient Idempotenz. Wiederholung derselben ID mit identischem Inhalt liefert dasselbe Ergebnis. Abweichender Inhalt mit gleicher ID wird als Konflikt abgelehnt.

## Befehlsannahme

Der Server antwortet bei angenommenem asynchronem Befehl mit `202 Accepted`:

```json
{
  "commandId": "cmd_44",
  "clientCommandId": "01J...",
  "status": "accepted",
  "acceptedAt": "2026-07-22T12:00:00Z",
  "acceptedStateVersion": 1844,
  "resource": "/api/v1/campaigns/cmp_1/commands/cmd_44"
}
```

Ein unmittelbar vollständig ausgeführter Befehl darf `200 OK` liefern, verwendet aber dieselbe Befehlsressource.

## Befehlsstatus

```text
GET    /api/v1/campaigns/{campaignId}/commands/{commandId}
DELETE /api/v1/campaigns/{campaignId}/commands/{commandId}
```

Zulässige Zustände:

- `accepted`,
- `scheduled`,
- `running`,
- `completed`,
- `rejected`,
- `failed`,
- `cancelled`.

`DELETE` bedeutet fachlichen Abbruchwunsch, nicht Löschen der Historie. Der Server antwortet mit dem tatsächlich erreichten Zustand und möglichen Kostenfolgen.

## Validierungsreihenfolge

Jeder Befehl wird mindestens geprüft auf:

1. gültige Session,
2. Kampagnenzugriff,
3. Controller- und Reichsberechtigung,
4. bekannte und zulässige Zielressourcen,
5. syntaktisch gültigen Befehlstyp und Payload,
6. fachliche Voraussetzungen,
7. verfügbare Ressourcen und Kapazitäten,
8. erwartete Zustandsversion, sofern erforderlich,
9. Idempotenz.

Der Client erhält keine Fehlermeldung, die unbekannte Ressourcen oder fremde Geheimnisse bestätigt.

## Nebenläufigkeit

`expectedStateVersion` kann bei konfliktanfälligen Befehlen verlangt werden. Ist die sichtbare Ausgangslage überholt, antwortet der Server mit `409 Conflict` und einer sicheren Aktualisierungsempfehlung.

Nicht jeder inzwischen erfolgte Zustandswechsel macht einen Befehl ungültig. Der Server prüft die tatsächlich betroffenen Voraussetzungen, nicht nur globale Versionsgleichheit.

## Fehlerformat

Alle fachlichen und technischen Fehler verwenden ein gemeinsames Format:

```json
{
  "error": {
    "code": "COMMAND_PRECONDITION_FAILED",
    "message": "Der Befehl kann im aktuellen Zustand nicht ausgeführt werden.",
    "correlationId": "cor_...",
    "details": [
      {
        "field": "payload.targetSystemId",
        "reason": "TARGET_NOT_REACHABLE"
      }
    ],
    "retryable": false,
    "currentStateVersion": 1846
  }
}
```

`message` ist für Menschen verständlich und lokalisierbar. `code` und `reason` sind stabile maschinenlesbare Kennungen.

## HTTP-Statuscodes

- `200 OK`: erfolgreiche Abfrage oder sofort ausgeführter Befehl.
- `201 Created`: neue Ressource dauerhaft erstellt.
- `202 Accepted`: Befehl angenommen, Ausführung läuft oder ist geplant.
- `204 No Content`: erfolgreiche Aktion ohne Antwortkörper.
- `304 Not Modified`: sichtbarer Zustand unverändert.
- `400 Bad Request`: syntaktisch oder strukturell ungültig.
- `401 Unauthorized`: keine gültige Session.
- `403 Forbidden`: Identität bekannt, aber keine Berechtigung.
- `404 Not Found`: Ressource nicht vorhanden oder aus Wissensschutz nicht offenlegbar.
- `409 Conflict`: Zustands-, Idempotenz- oder Nebenläufigkeitskonflikt.
- `422 Unprocessable Entity`: fachliche Voraussetzungen nicht erfüllt.
- `429 Too Many Requests`: begrenzte Wiederholung oder Rate Limit.
- `500 Internal Server Error`: unerwarteter Serverfehler ohne interne Details.
- `503 Service Unavailable`: vorübergehend nicht verfügbar oder Kampagne in Wartung.

## Pagination

Sammlungen verwenden Cursor-Pagination:

```text
GET /fleets?limit=50&cursor=...
```

Antworten enthalten `nextCursor` und keine instabilen Seitenzahlen. Sortierung ist dokumentiert und besitzt einen stabilen ID-Tie-Breaker.

## Löschung und Historie

Fachliche Entitäten werden nicht automatisch physisch gelöscht, wenn Historie, Berichte oder Referenzen sie benötigen. REST `DELETE` löst die fachlich definierte Aktion wie Abbruch, Aufgabe oder Ausmusterung aus.

## Rückkehrberichte

```text
GET /api/v1/campaigns/{campaignId}/reports/return?afterVersion=...
GET /api/v1/campaigns/{campaignId}/reports/campaign-final
```

Rückkehrberichte sind serverseitig priorisierte Zusammenfassungen. Sie ersetzen nicht den autoritativen Detailzustand und enthalten nur Wissen des Reiches.

## Administrationsschnittstellen

Administrative Operationen werden getrennt von regulären Spielbefehlen bereitgestellt und benötigen eigene Berechtigungen. Sie dürfen nicht über normale Reichscontroller erreichbar sein.

## Datenschutz und Protokollierung

Protokolliert werden Befehls-ID, Account, Reich, Kampagne, Befehlstyp, Annahmezeitpunkt, Ergebniscode und Korrelations-ID. Geheimnisse, Zugangstoken, vollständige private Inhalte oder interne AI-Gedankenketten werden nicht protokolliert.

## Anforderungen an Client

Der Client muss:

- Serverantworten als einzige Bestätigung verwenden,
- Befehle mit stabiler `clientCommandId` wiederholen können,
- `202` und Befehlsstatus unterstützen,
- Zustandsversionen, ETags und Änderungssynchronisation nutzen,
- unbekannte Felder tolerieren,
- Fehlercodes in verständliche Rückmeldungen übersetzen,
- niemals Informationen aus fehlenden oder verborgenen Feldern erraten.

## Anforderungen an Server

Der Server muss:

- alle Antworten nach Zugriff und Reichswissen filtern,
- Befehle idempotent und deterministisch validieren,
- Zustandsänderungen atomar versionieren,
- Änderungshistorie für einen dokumentierten Zeitraum bereitstellen,
- sichere Fehler ohne Informationslecks liefern,
- gleiche fachliche Befehle für Spieler und AI bereitstellen,
- API- und Definitionsversionen nachvollziehbar speichern.

## Offene Implementierungsentscheidungen

Diese Punkte ändern den fachlichen Vertrag nicht und werden bei der OpenAPI-Umsetzung festgelegt:

1. konkrete Token-Technologie,
2. maximale Long-Polling-Dauer,
3. Aufbewahrungszeit der Änderungshistorie,
4. genaue Ressourcenaufteilung großer Antworten,
5. Rate-Limits und technische Größenlimits,
6. OpenAPI-Dateistruktur und Codegenerierung.

## Akzeptanzkriterien

- Ressourcenmodell und Hauptoperationen sind fachlich definiert.
- Authentifizierung, Kampagnenzugriff und Reichscontroller sind getrennt.
- Spielzustand ist reichsspezifisch und versioniert abrufbar.
- Befehle sind idempotent, asynchron verfolgbar und serverautoritativ.
- Fehlerformat, Statuscodes, Pagination und Konflikte sind einheitlich.
- Inkrementelle Aktualisierung funktioniert über REST und benötigt keine WebSocket-Schnittstelle.
- Der Vertrag lässt sich in eine konkrete OpenAPI-v1-Spezifikation überführen.

## Fachliche Grundlagen

- [Zeitmodell](../../docs/01-gameplay/zeitmodell.md)
- [Erkundung und Informationsstände](../../docs/02-galaxy/erkundung-und-informationsstaende.md)
- [Reichsverwaltung](../../docs/03-empires/reichsverwaltung.md)
- [Planeten und Kolonien](../../docs/04-planets/planeten-und-kolonien.md)
- [Bevölkerung und Arbeit](../../docs/05-population/bevoelkerung-und-arbeit.md)
- [Wirtschaft und Versorgung](../../docs/06-economy/wirtschaft-und-versorgung.md)
- [Forschung und Technologien](../../docs/07-research/forschung-und-technologien.md)
- [Flotten und Raumkampf](../../docs/08-fleets/flotten-und-raumkampf.md)
- [Diplomatie und Krieg](../../docs/09-diplomacy/diplomatie-und-krieg.md)
- [Ereignisse und Krisen](../../docs/10-events/ereignisse-und-krisen.md)
- [Endgame und Abschluss](../../docs/11-campaign/endgame-und-abschluss.md)
