# Designprinzipien und Nicht-Ziele

Status: Freigegeben

## Zweck

Dieses Dokument definiert stabile Leitplanken für spätere Fachentscheidungen in **Galaxis**. Einzelne Systeme dürfen diese Prinzipien konkretisieren, aber nicht stillschweigend umgehen.

## Verbindliche Designprinzipien

### 1. Bedeutende Entscheidungen statt dauernder Eingaben

Spielzeit soll vor allem durch Abwägen, Priorisieren und Planen wertvoll werden. Fortschritt darf nicht davon abhängen, dass der Spieler dieselbe kleine Handlung häufig wiederholt.

**Prüffrage:** Erzeugt eine Mechanik eine echte Entscheidung oder nur zusätzliche Bedienarbeit?

### 2. Asynchron spielbar ohne Anwesenheitswettbewerb

Galaxis muss sinnvoll spielbar bleiben, wenn der Spieler nicht dauerhaft online ist. Häufigeres Nachsehen darf mehr Information und Planungstiefe ermöglichen, aber nicht automatisch durch bloße Anwesenheit überlegen sein.

**Prüffrage:** Entsteht ein unverhältnismäßiger Vorteil allein durch häufigere Kontrolle?

### 3. Strategische Kontrolle, automatisierbare Routine

Der Spieler bestimmt Ziele, Prioritäten und bedeutende Befehle. Wiederkehrende Routinen sollen automatisierbar, delegierbar oder gebündelt sein. Automatisierung muss nachvollziehbar bleiben und darf keine verborgenen Regeln verwenden.

**Prüffrage:** Behält der Spieler Kontrolle über die Richtung, ohne jede Routine manuell auszuführen?

### 4. Verständliche Folgen und sichtbarer Spielzustand

Relevante Ursachen, erwartbare Folgen, laufende Befehle und eingetretene Veränderungen müssen nachvollziehbar dargestellt werden können. Verborgene Informationen sind zulässig, willkürlich wirkende Ergebnisse nicht.

**Prüffrage:** Kann der Spieler verstehen, warum eine bedeutsame Veränderung eingetreten ist?

### 5. Tiefe durch Wechselwirkungen, nicht durch unnötige Menge

Strategische Tiefe soll aus dem Zusammenspiel weniger klarer Systeme entstehen. Neue Ressourcen, Werte, Gebäude oder Sonderregeln benötigen einen eigenständigen spielerischen Zweck.

**Prüffrage:** Eröffnet das neue Element eine neue Entscheidung oder verdoppelt es nur eine bestehende Funktion?

### 6. Serverautoritative und deterministisch prüfbare Regeln

Der Server ist die verbindliche Instanz für Simulation, Zeit, Zufall und Befehlsvalidierung. Gleiche Ausgangslagen und gleiche autoritative Eingaben müssen reproduzierbar ausgewertet werden können.

**Prüffrage:** Kann die Regel unabhängig vom Client eindeutig validiert und getestet werden?

### 7. Gleiche fachliche Befehle für Spieler und AI

Menschliche und AI-Controller verwenden dieselben fachlichen Befehle und unterliegen denselben Spielregeln. Unterschiede dürfen nur in der Auswahl der Befehle liegen, nicht in einer zweiten Simulationslogik.

**Prüffrage:** Könnte derselbe gültige Befehl auch vom jeweils anderen Controller erteilt werden?

### 8. Informationen in verständlichen Ebenen

Der Spieler soll zuerst entscheidungsrelevante Informationen erhalten und bei Bedarf tiefer einsteigen können. Komplexität darf verfügbar sein, ohne jede grundlegende Entscheidung zu überladen.

**Prüffrage:** Ist die wichtigste Aussage erkennbar, bevor alle Detailwerte gelesen werden?

### 9. Singleplayer zuerst, gemeinsame Grundlage für späteren Multiplayer

Die erste spielbare Ausbaustufe wird als Singleplayer entwickelt. Fachliche Regeln sollen so gestaltet sein, dass spätere Spielerübernahmen von AI-Reichen möglich sind, ohne die bestehende Simulation grundsätzlich zu ersetzen.

**Prüffrage:** Ist die Regel im Singleplayer sinnvoll und später mit mehreren Controllern vereinbar?

### 10. Kleine, klar abgegrenzte Ausbaustufen

Neue Systeme sollen einen spielbaren Nutzen liefern, bevor zusätzliche Tiefe ergänzt wird. Umfang allein ist kein Qualitätsmerkmal.

**Prüffrage:** Ist die kleinste sinnvolle Version des Systems klar erkennbar?

## Bewusste Nicht-Ziele

Galaxis verfolgt vorerst ausdrücklich nicht folgende Ziele:

- reflexbasierte Echtzeitkämpfe oder dauerhaftes taktisches Mikromanagement,
- Fortschritt durch Klickwiederholung, permanente Timerkontrolle oder Anwesenheitszwang,
- eine endlose Ranglistenökonomie als alleinigen Spielzweck,
- vollständige Simulation jedes realen astrophysikalischen, gesellschaftlichen oder wirtschaftlichen Details,
- maximale Anzahl an Ressourcen, Gebäuden, Schiffstypen oder Technologien ohne eigenständigen Zweck,
- unterschiedliche Spielregeln für menschliche und AI-gesteuerte Reiche,
- eine zweite verbindliche Regellogik im Client,
- vollständige Funktionsbreite eines großen kommerziellen Grand-Strategy-Spiels bereits im MVP,
- verpflichtende Nutzung experimenteller Ideen aus `ideas/`.

## Bekannte Spannungsfelder

### Tiefe gegen Zugänglichkeit

Im Konfliktfall soll die strategische Tiefe erhalten bleiben, aber über gestufte Informationen und klare Zusammenfassungen zugänglich gemacht werden. Das Verbergen wichtiger Regeln ist keine zulässige Vereinfachung.

### Automatisierung gegen Kontrolle

Automatisierung darf Bedienaufwand reduzieren, aber keine bedeutende Richtungsentscheidung eigenmächtig und unsichtbar ersetzen. Ziele und Grenzen automatisierter Abläufe müssen erkennbar sein.

### Persistente Entwicklung gegen Abwesenheitsschutz

Die Spielwelt soll sich weiterentwickeln, ohne kurze Abwesenheiten unverhältnismäßig zu bestrafen. Schutz darf umgekehrt nicht durch bewusstes Offlinegehen einen Vorteil erzeugen.

### Singleplayer-Freiheit gegen Multiplayer-Kompatibilität

Singleplayer darf zusätzliche Steuerungsmöglichkeiten wie eine ausdrückliche Pause besitzen. Die zugrunde liegenden Befehle und Zustandsübergänge müssen dennoch auf einem gemeinsamen Zeit- und Controller-Modell beruhen.

## Akzeptanzkriterien

- Jedes Prinzip ist durch eine konkrete Prüffrage bewertbar.
- Die Nicht-Ziele begrenzen unnötige Ausweitung und Kleinstverwaltung.
- Zentrale Konflikte zwischen Tiefe, Automatisierung, Persistenz und Multiplayer-Kompatibilität sind benannt.
- Spätere Fachentscheidungen können ausdrücklich auf diese Leitplanken verweisen.

## Verwandte Dokumente

- [Spielvision von Galaxis](game-vision.md)
- [Zielgruppe und gewünschtes Spielerlebnis](zielgruppe-und-spielerlebnis.md)
- [Verbindlicher Arbeitsworkflow](../../WORKFLOW.md)
