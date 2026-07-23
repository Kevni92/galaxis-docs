# Verbindlicher Arbeitsworkflow für Galaxis

Dieses Dokument beschreibt den verbindlichen Arbeitsablauf zwischen den Repositories:

- `galaxis-docs` – fachliche Quelle und Verträge,
- `galaxis-server` – serverautoritative Simulation und REST-Schnittstelle,
- `galaxis-client` – Desktop-Webclient.

Ein späterer Mobile-Client wird als eigenes Repository umgesetzt und verwendet dieselben fachlichen Dokumente und REST-Verträge.

> **Grundregel:** Eine Spielregel wird zuerst fachlich dokumentiert und freigegeben. Erst danach wird ihre Umsetzung in Client und Server geplant.

## 1. Verantwortlichkeiten der Repositories

### `galaxis-docs`

Enthält:

- Spielvision und Designprinzipien,
- Spielmechaniken und fachliche Regeln,
- Entitäten, Zustände und Beziehungen,
- Spieler- und AI-Befehle,
- sichtbare und verborgene Informationen,
- fachliche REST-Verträge,
- Designentscheidungen,
- versionierte Balancingziele, Formeln und Referenzszenarien,
- projektübergreifenden Arbeits- und Testprozess.

Das Repository enthält keinen produktiven Client- oder Servercode.

### `galaxis-server`

Verantwortet:

- serverautoritative Spielsimulation,
- Validierung aller Befehle,
- Zeit, Persistenz und Zufall,
- AI-Controller,
- REST-Endpunkte gemäß freigegebenem Vertrag,
- serverseitige Tests.

### `galaxis-client`

Verantwortet:

- Desktop-Bedienoberfläche,
- Darstellung des vom Server freigegebenen Spielzustands,
- Eingabe und Übermittlung fachlicher Befehle,
- verständliche Rückmeldungen und Fehlerdarstellung,
- clientseitige Tests.

Der Client darf keine serverseitigen Spielregeln als eigene verbindliche Wahrheit nachbilden. Lokale Vorprüfungen dienen nur der Bedienbarkeit; der Server bleibt maßgeblich.

## 2. Verbindliche Quellenreihenfolge

1. angenommene Designentscheidung unter `decisions/`,
2. freigegebener Vertrag unter `contracts/`,
3. freigegebenes Fachdokument unter `docs/`,
4. freigegebene oder als Baseline gekennzeichnete Balancingquelle unter `balancing/`,
5. Dokument im Review,
6. Entwurf,
7. Issue, PR-Kommentar oder Chat.

Ein Issue ersetzt keine freigegebene Fachregel. Inhalte unter `ideas/` besitzen keine fachliche Wirkung. Balancingquellen dürfen höher priorisierte Fachregeln nicht verändern.

## 3. Lebenszyklus eines Features

### Schritt 1: Fachliches Docs-Issue

Jedes größere Feature beginnt als Issue in `galaxis-docs`.

Beispiel:

> Flottenbefehl „Sternensystem erkunden“ fachlich definieren

Das Issue benennt:

- Ziel und Abgrenzung,
- betroffenen Dokumentationsbereich,
- offene Entscheidungen,
- erwartete Dokumente,
- fachliche Akzeptanzkriterien.

### Schritt 2: Fachlichen Entwurf erstellen

Die passende Vorlage unter `templates/` wird verwendet. Der Entwurf beschreibt mindestens:

- Zweck und Spielerwirkung,
- Voraussetzungen,
- Ablauf und Regeln,
- Zustände und Übergänge,
- Kosten, Dauer und Ergebnisse,
- Fehler- und Sonderfälle,
- sichtbare und verborgene Informationen,
- Wechselwirkungen mit anderen Systemen,
- fachliche Anforderungen an Client und Server,
- testbare Akzeptanzkriterien,
- offene Fragen.

Fehlende Regeln dürfen nicht erfunden oder stillschweigend angenommen werden.

### Schritt 3: Designentscheidungen festhalten

Grundlegende oder langfristig folgenreiche Entscheidungen werden unter `decisions/` dokumentiert.

Beispiele:

- Zeitmodell,
- Offline-Fortschritt,
- Kriegs- und Abwesenheitsschutz,
- Eigentum und Controller eines Reiches,
- deterministischer Zufall,
- Grenzen zwischen Client und Server.

### Schritt 4: Fachliche Freigabe

Ein Dokument darf erst auf `Freigegeben` gesetzt werden, wenn:

- keine ungeklärte Kernregel als verbindlich dargestellt wird,
- Begriffe dem Glossar entsprechen,
- Widersprüche geklärt oder sichtbar dokumentiert sind,
- Client- und Serverauswirkungen beschrieben sind,
- Akzeptanzkriterien testbar sind,
- Navigation und Querverweise stimmen.

### Schritt 5: Feature-ID vergeben

Repositoryübergreifende Features erhalten eine stabile Kennung.

Format:

```text
GAL-<BEREICH>-<FEATURE>-<NUMMER>
```

Beispiel:

```text
GAL-FLEET-EXPLORE-001
```

Die Kennung wird in Docs-, Client- und Server-Issues sowie in relevanten Tests verwendet.

### Schritt 6: REST-Vertrag definieren

Bevor Client und Server unabhängig implementieren, wird der fachliche Vertrag unter `contracts/rest-api/` festgelegt.

Er beschreibt mindestens:

- Endpunkt und fachlichen Zweck,
- Request- und Response-Struktur,
- Berechtigungen,
- Validierungs- und Fehlerfälle,
- Sichtbarkeit von Daten,
- Nebenwirkungen,
- Kompatibilitätsanforderungen.

Später soll daraus eine maschinenlesbare OpenAPI-Spezifikation entstehen.

### Schritt 7: Umsetzungs-Issues ableiten

Aus dem freigegebenen Fachkonzept entstehen getrennte Issues in `galaxis-server` und `galaxis-client`.

Jedes Umsetzungs-Issue verlinkt:

- Feature-ID,
- fachliches Docs-Issue,
- maßgebliches Fachdokument,
- REST-Vertrag,
- zugehöriges Issue im anderen Repository,
- relevante Designentscheidungen,
- erwartete Tests.

### Schritt 8: Umsetzung in kleinen PRs

PRs sollen eine klar abgegrenzte Änderung enthalten. Große Features werden aufgeteilt, zum Beispiel in:

1. Domainmodell oder Zustandslogik,
2. Serverbefehl und Validierung,
3. Persistenz,
4. REST-Endpunkt,
5. Client-API-Anbindung,
6. Client-Komponente,
7. Integration und kritischer E2E-Ablauf.

Eine PR darf nicht mehrere unabhängige Features nur deshalb zusammenfassen, weil sie von derselben Agent-Session bearbeitet werden.

#### Verbindlicher Branch- und PR-Ablauf

Für alle Arbeits- und Agenten-Sessions gilt:

1. Vor jedem neuen Issue wird der aktuelle Stand geladen:

   ```bash
   git fetch origin --prune
   git switch main
   git pull --ff-only origin main
   git status
   ```

2. Der Arbeitsbaum muss sauber sein. Ein neuer Issue-Branch wird ausschließlich vom aktuellen `origin/main` erstellt.
3. Jeder Pull Request verwendet ausschließlich `main` als Base.
4. Ein Feature- oder Issue-Branch darf niemals Base eines weiteren Feature-PRs sein.
5. Gestapelte Pull Requests und das Mergen eines Feature-Branches in einen anderen Feature-Branch sind verboten, außer der Nutzer ordnet dies für einen konkreten Fall ausdrücklich an.
6. Das nächste Issue darf erst begonnen werden, wenn der vorherige PR nach `main` gemergt, die erforderliche CI erfolgreich und das lokale `main` erneut aktualisiert wurde.
7. Ist der vorherige PR noch offen oder nicht nach `main` gemergt, stoppt der Agent. Er setzt die nächste Aufgabe weder auf demselben Branch noch auf einem davon abgeleiteten Branch fort.
8. Ein PR wird ausdrücklich mit `main` als Base erstellt, beispielsweise:

   ```bash
   gh pr create --base main --head <BRANCH>
   ```

9. Nach dem Erstellen wird die Base geprüft:

   ```bash
   gh pr view <PR-NUMMER> --json baseRefName,headRefName
   ```

   `baseRefName` muss exakt `main` sein. Andernfalls wird nicht weitergearbeitet, bis der PR korrigiert ist.
10. Jeder PR, der ein Issue vollständig umsetzt, muss in der PR-Beschreibung ein GitHub-Closing-Keyword in eigener Zeile enthalten, bevorzugt `Closes #<ISSUE-NUMMER>`. Eine Feature-ID, ein Link, eine Erwähnung im Titel oder Text wie „Issue #…“ ersetzt dieses Closing-Keyword nicht. Werden mehrere Issues vollständig erledigt, wird jedes mit einem eigenen Closing-Keyword angegeben.
11. Vor Abschluss der Agenten-Session wird mit `gh pr view <PR-NUMMER> --json body` geprüft, dass das korrekte Closing-Keyword tatsächlich in der veröffentlichten PR-Beschreibung steht. Fehlt es, muss die PR-Beschreibung vor dem Abschluss korrigiert werden.
12. Nach erfolgreichem Merge darf der Feature-Branch erst gelöscht werden, wenn seine relevanten Änderungen nachweislich in `origin/main` enthalten sind und kein offener PR den Branch mehr verwendet.
13. Bestehende versehentlich gestapelte Branches werden ohne Umschreiben von `main` repariert: Ein neuer Reparaturbranch startet vom aktuellen `origin/main` und übernimmt ausschließlich die fehlenden normalen Commits. Merge-Commits der alten Stapelkette werden nicht übernommen.

### Schritt 9: Testen und Review

Jede PR folgt der verbindlichen Strategie aus [`TESTING.md`](TESTING.md).

Die PR-Beschreibung nennt:

- betroffene Feature-ID,
- fachliche Quelle,
- Änderung und Abgrenzung,
- ausgeführte Tests,
- bewusst nicht ausgeführte Tests mit Begründung,
- mögliche Risiken oder Folgearbeiten,
- für jedes vollständig umgesetzte Issue ein Closing-Keyword, bevorzugt `Closes #<ISSUE-NUMMER>`.

### Schritt 10: Merge und Nachführung

Nach dem Merge:

- werden die durch Closing-Keywords verknüpften Issues automatisch geschlossen und ihr Status kontrolliert,
- werden neue Erkenntnisse in `galaxis-docs` zurückgeführt,
- wird bei Vertragsänderungen geprüft, ob Client und Server angepasst werden müssen,
- wird das Docs-Submodule in Client und Server bewusst auf einen freigegebenen Commit aktualisiert.

Submodule-Updates dürfen nicht nebenbei oder ohne Prüfung erfolgen.

## 4. Arbeit mit dem Docs-Submodule

`galaxis-client` und `galaxis-server` binden `galaxis-docs` als Git-Submodule ein.

Regeln:

- Das Submodule zeigt immer auf einen konkreten Commit.
- Eine Agent-Session liest vor der Umsetzung die eingebundene Dokumentation.
- Bei veralteter Dokumentation wird nicht gegen einen vermuteten neuen Stand implementiert.
- Ein Submodule-Update ist eine sichtbare Änderung im PR.
- Fachliche Änderungen erfolgen im Docs-Repository, nicht in der eingebundenen Kopie.

## 5. Start einer Agent-Session

Ein Agent muss vor der Arbeit:

1. `AGENTS.md` lesen,
2. dieses Dokument lesen,
3. [`TESTING.md`](TESTING.md) lesen,
4. Repository und aktuelle Aufgabe identifizieren,
5. Git-Ausgangslage gemäß dem verbindlichen Branch- und PR-Ablauf prüfen,
6. maßgebliche Docs-Dateien und Entscheidungen lesen,
7. vorhandene Modul-READMEs und Code-Navigationen lesen,
8. Abhängigkeiten und betroffene Tests bestimmen,
9. die Änderung auf den kleinsten sinnvollen Umfang begrenzen.

## 6. Anforderungen an Client- und Serverstruktur

Für Vibecoding gelten in beiden Umsetzungs-Repositories:

- Module besitzen klar abgegrenzte Verantwortlichkeiten.
- Übergroße Klassen und zentrale Sammelmodule sind zu vermeiden.
- Abhängigkeiten zwischen Modulen müssen sichtbar und begründet sein.
- Sinnvolle `src`-Unterordner erhalten ein `README.md` als Inhalts- und Navigationsübersicht.
- Diese README-Dateien beschreiben Zweck, wichtige Module, Klassen, Funktionen, Datenflüsse und Einstiegspunkte.
- Nach Verschieben oder Umbenennen von Code muss die Navigation aktualisiert werden.
- Fachbegriffe aus `galaxis-docs` werden konsistent verwendet.

## 7. Definition of Done einer Umsetzungsaufgabe

Eine Aufgabe ist abgeschlossen, wenn:

- die freigegebene Fachregel erfüllt ist,
- keine nicht dokumentierte Spielregel eingeführt wurde,
- Client und Server den vereinbarten Vertrag einhalten,
- passende schnelle Tests vorhanden sind,
- ein kritischer neuer Nutzerablauf bei Bedarf durch E2E abgedeckt ist,
- bestehende Tests erfolgreich sind,
- Modulnavigation und Dokumentation aktualisiert sind,
- keine bekannten relevanten Fehler verschwiegen werden,
- das Issue und die PR die Feature-ID und Quellen enthalten,
- die PR-Beschreibung das korrekte Closing-Keyword für jedes vollständig erledigte Issue enthält,
- der PR nach `main` gerichtet ist und kein Folge-Issue auf seinem Feature-Branch begonnen wurde.

## 8. Rückfluss von Erkenntnissen

Während der Umsetzung entdeckte fachliche Lücken werden nicht dauerhaft nur im Client- oder Servercode gelöst.

Stattdessen:

1. Lücke im Umsetzungs-Issue dokumentieren,
2. Docs-Issue oder Designentscheidung erstellen,
3. fachliche Quelle ergänzen und freigeben,
4. anschließend Umsetzung anpassen.

So bleibt `galaxis-docs` die langfristige gemeinsame Wahrheit.

## 9. Balancing-Lebenszyklus

Balancingänderungen folgen zusätzlich dem verbindlichen Ablauf aus [`balancing/workflow.md`](balancing/workflow.md).

Dabei gilt:

1. beobachtetes Verhalten und Spielerwirkung beschreiben,
2. Ausgangsmetriken mit Version, Szenario und Seeds sichern,
3. Änderungshypothese und Zielkorridor formulieren,
4. Werte in versionierten Serverdaten ändern,
5. Formeln, Erhaltung, Determinismus und Referenzszenarien testen,
6. Vorher-/Nachher-Bericht erstellen,
7. Playtestbedarf bewerten,
8. Balancingstatus, Version und Changelog aktualisieren,
9. Savegame-, Migrations- und Rollbackwirkung dokumentieren.

Eine Balancingänderung, die eine neue Spielregel, Berechtigung, Information oder Zustandsbedeutung benötigt, kehrt vor der Umsetzung zum fachlichen Docs-Workflow zurück.