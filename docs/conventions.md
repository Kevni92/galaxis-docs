# Dokumentationskonventionen

## 1. Sprache

Alle fachlichen Dokumente werden auf Deutsch geschrieben. Fachbegriffe aus Technik oder Spielentwicklung dürfen verwendet werden, wenn sie im Glossar erklärt werden oder allgemein eindeutig sind.

## 2. Dateinamen

- ausschließlich Kleinbuchstaben,
- Wörter mit Bindestrichen trennen,
- Dateiendung `.md`,
- keine Versionsnummer im Dateinamen,
- ein Dokument behandelt ein klar abgegrenztes Thema.

Beispiel: `planetare-gebaeude.md`

## 3. Dokumentstatus

Jedes eigenständige Fachdokument beginnt mit:

```markdown
Status: Entwurf
```

Erlaubte Status:

- **Entwurf**: unvollständig oder fachlich noch offen,
- **Review**: vollständig genug für eine fachliche Prüfung,
- **Freigegeben**: verbindliche Grundlage für die Umsetzung,
- **Ersetzt**: nicht mehr gültig; verweist auf den Nachfolger,
- **Verworfen**: bewusst nicht weiterverfolgt.

Ein `README.md` als reine Navigation benötigt keinen Status.

## 4. Pflichtstruktur

Fachdokumente enthalten, soweit fachlich sinnvoll:

1. Status,
2. Zweck,
3. Begriffe und Abgrenzung,
4. Voraussetzungen,
5. Regeln und Ablauf,
6. Zustände und Übergänge,
7. Wechselwirkungen,
8. Sonderfälle und Grenzen,
9. sichtbare Informationen,
10. Anforderungen an Client und Server,
11. offene Fragen,
12. Akzeptanzkriterien,
13. verwandte Dokumente.

Passende Vorlagen liegen unter [`templates/`](../templates/README.md).

## 5. Normative Formulierungen

- **muss**: verbindlich,
- **darf nicht**: verboten,
- **soll**: bevorzugt, begründete Ausnahme möglich,
- **kann**: optional,
- **Beispiel**: unverbindliche Veranschaulichung.

Unklare Formulierungen wie „normalerweise“, „irgendwie“, „meistens“ oder „geeignet“ müssen konkretisiert werden.

## 6. Verlinkung

- relative Markdown-Links verwenden,
- auf die maßgebliche Definition verlinken statt sie zu kopieren,
- verwandte Dokumente am Ende aufführen,
- bei neuen Dateien das nächstgelegene `README.md` aktualisieren.

## 7. Eine maßgebliche Quelle

Jede fachliche Regel besitzt genau ein maßgebliches Dokument. Andere Dokumente verweisen darauf und beschreiben höchstens die eigene Wechselwirkung.

## 8. Offene Fragen

Offene Fragen werden als nummerierte Liste geführt. Zu jeder Frage sollen betroffene Bereiche und bekannte Alternativen genannt werden.

Offene Fragen dürfen nicht als bereits beschlossene Regeln in Verträge oder Umsetzungs-Issues übernommen werden.

## 9. Annahmen und Beispiele

Annahmen werden mit **Annahme:** gekennzeichnet. Beispiele werden mit **Beispiel:** gekennzeichnet. Beide sind nicht verbindlich.

## 10. Freigabe

Ein Dokument kann auf `Freigegeben` gesetzt werden, wenn:

- keine entscheidungsrelevanten Widersprüche bestehen,
- alle verbindlichen Begriffe definiert sind,
- Regeln, Eingaben, Ergebnisse und Sonderfälle nachvollziehbar sind,
- offene Fragen die Umsetzung nicht blockieren,
- daraus konkrete Client- und Server-Issues abgeleitet werden können,
- Querverweise und Navigation aktuell sind.
