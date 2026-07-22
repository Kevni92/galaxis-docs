# Verbindliche Kommunikation einer Agenten-Session

Dieses Dokument legt fest, wie ein Agent den Beginn und Abschluss einer Issue-Umsetzung gegenüber dem Benutzer kommuniziert. Es gilt für `galaxis-docs`, `galaxis-server` und `galaxis-client`.

## 1. Aufgabenbeschreibung vor der Umsetzung

Nachdem der Agent das Issue, `AGENTS.md`, `WORKFLOW.md`, die maßgeblichen Quellen und die unmittelbaren Abhängigkeiten gelesen hat, muss er **vor der ersten inhaltlichen Änderung** eine kurze Aufgabenbeschreibung ausgeben.

Überschrift:

```text
## Aufgabenverständnis
```

Anforderungen:

- ungefähr 80 bis 120 Wörter, möglichst nicht mehr als 100 Wörter,
- kurze, verständliche Sätze,
- nennt Repository und Issue,
- beschreibt Ziel und erwartetes Ergebnis,
- nennt die wichtigsten Grenzen oder Nicht-Ziele,
- erwähnt wesentliche Abhängigkeiten nur, wenn sie die Umsetzung beeinflussen,
- enthält noch keine ausführliche technische Lösung und keinen langen Arbeitsplan.

Beispiel:

> In `galaxis-server#3` wird die technische Laufzeitgrundlage des Servers ergänzt. Der Server soll seine Konfiguration validieren, strukturierte Logs schreiben und getrennte Liveness- und Readiness-Endpunkte anbieten. Außerdem wird ein geordneter Start- und Shutdown-Ablauf vorbereitet. Gameplay, Accounts und Kampagnen gehören nicht zu diesem Issue. Die Umsetzung baut auf der Repositorybasis und den deterministischen Laufzeit-Providern auf.

## 2. Updates während längerer Arbeiten

Bei längeren Aufgaben darf der Agent kurze Zwischenstände geben. Diese sollen neue Erkenntnisse, gefundene Probleme oder bereits abgeschlossene Teilziele nennen. Reine Aktivitätsmeldungen ohne Informationswert sind zu vermeiden.

## 3. Abschlussbericht

Nach Abschluss oder Abbruch der Arbeit muss der Agent einen kurzen strukturierten Bericht ausgeben. Der Bericht soll normalerweise höchstens etwa 300 Wörter umfassen; reine Testbefehle dürfen zusätzlich aufgeführt werden.

Verbindliche Struktur:

```markdown
## Abschlussbericht

**Status:** Abgeschlossen | Teilweise abgeschlossen | Blockiert

### Umgesetzt
- Welche sichtbaren Ergebnisse wurden erreicht?

### Technische Umsetzung
- Wie wurde die Aufgabe im Wesentlichen gelöst?

### Tests
- `Befehl` – Ergebnis
- Nicht ausgeführte Prüfung – konkrete Begründung

### Offen oder Risiken
- Verbleibende Abweichungen, Risiken oder Folgearbeit
- `Keine bekannten offenen Punkte`, wenn nichts bekannt ist

### Empfohlene Fortsetzung
**Nächstes Issue:** `Repository#Nummer – Titel`

Zwei bis drei kurze Sätze dazu, warum dieses Issue als Nächstes folgt und was darin umgesetzt wird.

**Vorschlag:** Soll ich mit `Repository#Nummer` fortfahren?
```

## 4. Auswahl des nächsten Issues

Das nächste Issue wird nicht allein anhand der Nummer bestimmt. Der Agent prüft vor der Empfehlung:

1. die festgelegte Reihenfolge in Roadmap und Milestone,
2. Abhängigkeiten des aktuellen und möglichen nächsten Issues,
3. offenen oder geschlossenen Zustand,
4. erforderliche Docs- oder Vertragsarbeit,
5. Blocker und Erkenntnisse aus der gerade abgeschlossenen Umsetzung.

Regeln:

- Ist der reguläre Nachfolger offen und sind seine Voraussetzungen erfüllt, wird er empfohlen.
- Ist eine Voraussetzung noch offen, wird zuerst diese Voraussetzung empfohlen.
- Ist das aktuelle Issue nur teilweise abgeschlossen oder blockiert, wird zuerst die notwendige Entblockung genannt.
- Gibt es mehrere gleichwertige Aufgaben, wählt der Agent eine begründete Standardempfehlung und nennt höchstens eine Alternative.
- Gibt es keine belastbare Folgeaufgabe, lautet die Empfehlung: `Keine eindeutige nächste Aufgabe; Roadmap oder Umbrella-Issue prüfen.`
- Die Beschreibung des nächsten Issues umfasst höchstens zwei bis drei kurze Sätze und darf dessen vollständigen Inhalt nicht wiederholen.

## 5. Ehrlichkeit und Nachvollziehbarkeit

- Nur tatsächlich umgesetzte Änderungen werden als abgeschlossen bezeichnet.
- Nur tatsächlich ausgeführte Tests werden als ausgeführt genannt.
- Fehlgeschlagene oder ausgelassene Tests werden sichtbar aufgeführt.
- Commit, Push, PR und Issue-Abschluss werden nur behauptet, wenn sie tatsächlich erfolgt sind.
- Eine Empfehlung für das nächste Issue ist ein Vorschlag, keine Behauptung, dass seine Voraussetzungen automatisch erfüllt sind.
