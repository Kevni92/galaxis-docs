# Quellcodedokumentation

Diese Regeln gelten für `galaxis-client`, `galaxis-server` und alle späteren Umsetzungs-Repositories.

> **Grundregel:** Quellcode muss sich möglichst selbst erklären. Kommentare verbinden Code mit fachlichen Quellen oder erklären nicht offensichtliche Gründe – sie wiederholen nicht den Code.

## 1. Verweise im Dateikopf

Eine Quelldatei soll einen kurzen Dateikopf erhalten, wenn sie eine fachliche Entität, Mechanik, einen Befehl oder REST-Vertrag wesentlich umsetzt.

Der Dateikopf:

- steht vor dem eigentlichen Code,
- umfasst höchstens drei bis vier kurze Zeilen,
- enthält nur relevante Quellen,
- verwendet Pfade relativ zum Root des Umsetzungs-Repositories,
- wird bei fachlichen Änderungen aktualisiert.

Beispiel:

```text
// Feature: GAL-FLEET-EXPLORE-001
// Fachliche Grundlage: docs/docs/08-fleets/system-exploration.md
// REST-Vertrag: docs/contracts/rest-api/fleets/explore-system.md
```

Nicht fachliche Hilfs-, Konfigurations-, generierte oder rein technische Dateien benötigen keinen solchen Kopf.

## 2. Kommentare an Klassen und Funktionen

Kommentare sind nur erforderlich, wenn sie echten Zusatznutzen liefern, insbesondere für:

- öffentliche Schnittstellen,
- fachliche Invarianten,
- nicht offensichtliche Nebenwirkungen,
- begründete Einschränkungen,
- ungewöhnliche Entscheidungen oder Workarounds.

Dabei gilt:

- möglichst ein kurzer Satz,
- erklären, **warum** etwas nötig ist, nicht **was** die nächste Codezeile tut,
- keine Kommentare für triviale Getter, Setter oder selbsterklärende Abläufe,
- keine Kopie der fachlichen Dokumentation im Quellcode.

## 3. Modulnavigation

Sinnvolle `src`-Unterordner erhalten ein kurzes `README.md` als Navigationshilfe für Menschen und Agenten.

Es enthält nur:

- Zweck des Moduls,
- wichtigste Dateien, Klassen oder Einstiegspunkte,
- wesentliche Abhängigkeiten,
- Links auf relevante fachliche Dokumente.

Bevorzugtes Format:

```markdown
| Datei/Modul | Verantwortung | Fachliche Quelle |
|---|---|---|
| `ExploreSystemCommand` | Validiert und startet die Systemerkundung | `docs/docs/08-fleets/system-exploration.md` |
```

Das Modul-README ist kein Architekturaufsatz und keine vollständige API-Dokumentation.

## 4. Verbindliche Pflege

Bei einer Änderung muss geprüft werden, ob:

- der Dateikopf noch auf die richtigen Fachquellen verweist,
- neue fachlich relevante Dateien einen Verweis benötigen,
- verschobene oder umbenannte Dateien im Modul-README aktualisiert werden müssen,
- eine fachliche Erkenntnis zurück nach `galaxis-docs` gehört.

Veraltete Kommentare oder Links müssen in derselben PR korrigiert oder entfernt werden.

## 5. Nicht erlaubt

- mehrseitige Dokumentation direkt in Quelldateien,
- duplizierte Spielregeln in Kommentaren,
- Kommentare, die nur Code in natürliche Sprache übersetzen,
- erfundene Fachregeln, um fehlende Dokumentation zu umgehen,
- Links nur auf Issues, wenn bereits ein freigegebenes Fachdokument existiert.

## 6. Prüfung in Pull Requests

Eine PR mit fachlich relevantem Code prüft zusätzlich:

- [ ] Fachliche Quellen sind im Dateikopf verlinkt, sofern sinnvoll.
- [ ] Kommentare sind kurz und erklären nur zusätzlichen Kontext.
- [ ] Betroffene Modul-READMEs sind aktuell.
- [ ] Fachliche Regeln werden nicht im Code dupliziert.
