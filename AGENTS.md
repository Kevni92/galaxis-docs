# Agent-Anweisungen

1. Vor jeder Aufgabe lesen: `README.md`, `WORKFLOW.md`, `TESTING.md`, `SOURCE-CODE.md`, `docs/conventions.md` sowie die relevanten Fach-, Vertrags-, Entscheidungs- und Balancingdokumente.
2. `galaxis-docs` ist die fachliche Quelle. Fehlende oder widersprüchliche Spielregeln dürfen nicht erfunden oder stillschweigend entschieden werden.
3. Fachliche Änderungen verwenden die passende Vorlage unter `templates/`, die Begriffe aus `glossary.md` und aktualisieren die nächstgelegene Navigation.
4. Spielregeln werden zuerst dokumentiert und freigegeben; danach entstehen getrennte Client- und Server-Issues gemäß `WORKFLOW.md`.
5. Umsetzungs-Repositories müssen fachlich relevanten Quellcode knapp mit den maßgeblichen Docs verknüpfen und gemäß `TESTING.md` testen.
6. Inhalte unter `balancing/` dürfen nur Zahlen, Formeln, Kataloge und Zielkorridore konkretisieren. Sie dürfen Fachregeln, Berechtigungen, Informationsgrenzen oder Invarianten nicht verändern.
7. Jede produktive Balancingänderung benötigt Version, Quelle, Metrikziel, Referenzszenario, Vorher-/Nachher-Nachweis und Changelog-Eintrag.
8. Inhalte unter `ideas/` sind unverbindlich, keine fachliche Quelle und dürfen nur berücksichtigt werden, wenn eine Aufgabe ausdrücklich auf die jeweilige Idee verweist.
9. Fachliche und Balancingänderungen erfolgen im Docs-Repository, nicht in der eingebundenen Submodule-Kopie.
10. `CLAUDE.md` enthält keine eigenen Regeln und verweist nur auf diese Datei.