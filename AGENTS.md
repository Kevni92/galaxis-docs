# Arbeitsregeln für KI-Agenten

Diese Datei ist die zentrale Anweisung für Claude, Codex und andere KI-Agenten im Repository `galaxis-docs`.

## 1. Zweck des Repositories

Dieses Repository enthält ausschließlich die fachliche Dokumentation von Galaxis.

Beschrieben werden:

- Spielregeln und Mechaniken,
- fachliche Entitäten und deren Beziehungen,
- Spieler- und AI-Befehle,
- Zustände, Übergänge und Ereignisse,
- fachliche Anforderungen an Client, Server und REST-Schnittstelle,
- getroffene Designentscheidungen.

Nicht beschrieben werden konkrete Klassenstrukturen, Frameworkentscheidungen oder Implementierungsdetails des Clients oder Servers, sofern sie nicht als fachliche Einschränkung relevant sind.

## 2. Vor jeder Änderung lesen

Vor einer Änderung müssen mindestens gelesen werden:

1. `README.md`,
2. `docs/conventions.md`,
3. das `README.md` des betroffenen Themenbereichs,
4. relevante Einträge in `glossary.md`,
5. betroffene Entscheidungen unter `decisions/`,
6. vorhandene verwandte Dokumente und Verträge.

## 3. Quellenpriorität

Bei Widersprüchen gilt:

1. angenommene Designentscheidung,
2. freigegebenes Fachdokument,
3. freigegebener Vertrag,
4. Dokument im Review,
5. Entwurf,
6. Issue, Kommentar oder Diskussion.

Ein Agent darf einen Widerspruch nicht stillschweigend lösen. Er muss ihn ausdrücklich benennen und gegebenenfalls eine Designentscheidung vorbereiten.

## 4. Fachliche Entscheidungen

Ungeklärte Punkte dürfen nicht als verbindliche Regeln formuliert werden.

Verwende dafür den Abschnitt `Offene Fragen` und kennzeichne:

- welche Entscheidung fehlt,
- welche Bereiche betroffen sind,
- welche Alternativen bereits bekannt sind.

Grundlegende oder langfristig folgenreiche Entscheidungen werden zusätzlich unter `decisions/` dokumentiert.

## 5. Dokumente erstellen und ändern

- Verwende die passende Vorlage unter `templates/`.
- Schreibe auf Deutsch.
- Verwende die Begriffe aus `glossary.md`.
- Trenne fachliche Regeln von Beispielen und Umsetzungshinweisen.
- Formuliere Regeln eindeutig und überprüfbar.
- Verlinke verwandte Dokumente relativ.
- Aktualisiere das nächstgelegene `README.md`, wenn ein Dokument ergänzt, verschoben oder entfernt wird.
- Vermeide doppelte Definitionen. Eine Regel besitzt genau eine maßgebliche Quelle.

## 6. Normative Sprache

- `muss`: verbindliche Regel,
- `darf nicht`: verbindliches Verbot,
- `soll`: bevorzugtes Verhalten mit möglichen Ausnahmen,
- `kann`: optionale Möglichkeit,
- `Beispiel`: nicht verbindliche Veranschaulichung.

## 7. Trennung der Verantwortlichkeiten

Fachliche Dokumente dürfen Anforderungen an Client und Server nennen, aber keine konkrete Implementierung erzwingen, sofern keine fachliche Notwendigkeit besteht.

Beispiel:

- zulässig: „Der Server muss prüfen, ob der Spieler die Flotte kontrolliert.“
- unzulässig: „Die Prüfung muss in `FleetCommandService::validate()` erfolgen.“

## 8. Befehle und Controller

Spieler und AI steuern ein Reich über dieselben fachlichen Befehle. Dokumentationen dürfen keine Spielregel definieren, die ausschließlich deshalb anders funktioniert, weil ein Befehl von einem menschlichen oder einem AI-Controller stammt, außer dies ist ausdrücklich als Spielregel beschlossen.

## 9. Qualitätsprüfung

Vor Abschluss einer Änderung prüfen:

- Ist der Zweck klar?
- Sind Voraussetzungen, Regeln, Ergebnisse und Sonderfälle beschrieben?
- Sind Begriffe konsistent?
- Gibt es widersprüchliche Parallelbeschreibungen?
- Sind offene Fragen sichtbar?
- Können daraus Client- und Server-Issues abgeleitet werden?
- Wurden Navigation und Querverweise aktualisiert?

## 10. Keine eigenmächtige Erweiterung

Ein Agent darf fehlende Spielregeln nicht erfinden, um ein Dokument vollständig wirken zu lassen. Annahmen müssen ausdrücklich als Annahmen oder offene Fragen markiert werden.
