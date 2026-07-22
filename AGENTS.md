# Agent-Anweisungen

1. Vor jeder Aufgabe lesen: `README.md`, `WORKFLOW.md`, `AGENT-COMMUNICATION.md`, `TESTING.md`, `SOURCE-CODE.md`, `docs/conventions.md` sowie die relevanten Fach-, Vertrags-, Entscheidungs- und Balancingdokumente.
2. Nach dem Lesen der Aufgabe und ihrer Quellen, aber vor der ersten inhaltlichen Änderung, eine kurze Beschreibung unter `## Aufgabenverständnis` ausgeben. Sie umfasst ungefähr 80 bis 120 Wörter und beschreibt Ziel, Ergebnis, Grenzen und wesentliche Abhängigkeiten gemäß `AGENT-COMMUNICATION.md`.
3. Nach Abschluss oder Abbruch einen strukturierten `## Abschlussbericht` gemäß `AGENT-COMMUNICATION.md` ausgeben. Er nennt Status, Umsetzung, technische Vorgehensweise, tatsächlich ausgeführte Tests, offene Risiken und das begründet empfohlene nächste Issue mit einer Beschreibung in zwei bis drei Sätzen.
4. `galaxis-docs` ist die fachliche Quelle. Fehlende oder widersprüchliche Spielregeln dürfen nicht erfunden oder stillschweigend entschieden werden.
5. Fachliche Änderungen verwenden die passende Vorlage unter `templates/`, die Begriffe aus `glossary.md` und aktualisieren die nächstgelegene Navigation.
6. Spielregeln werden zuerst dokumentiert und freigegeben; danach entstehen getrennte Client- und Server-Issues gemäß `WORKFLOW.md`.
7. Umsetzungs-Repositories müssen fachlich relevanten Quellcode knapp mit den maßgeblichen Docs verknüpfen und gemäß `TESTING.md` testen.
8. Inhalte unter `balancing/` dürfen nur Zahlen, Formeln, Kataloge und Zielkorridore konkretisieren. Sie dürfen Fachregeln, Berechtigungen, Informationsgrenzen oder Invarianten nicht verändern.
9. Jede produktive Balancingänderung benötigt Version, Quelle, Metrikziel, Referenzszenario, Vorher-/Nachher-Nachweis und Changelog-Eintrag.
10. Inhalte unter `ideas/` sind unverbindlich, keine fachliche Quelle und dürfen nur berücksichtigt werden, wenn eine Aufgabe ausdrücklich auf die jeweilige Idee verweist.
11. Fachliche und Balancingänderungen erfolgen im Docs-Repository, nicht in der eingebundenen Submodule-Kopie.
12. `CLAUDE.md` enthält keine eigenen Regeln und verweist nur auf diese Datei.
