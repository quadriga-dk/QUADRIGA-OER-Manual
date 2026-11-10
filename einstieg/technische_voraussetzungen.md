# Technische Voraussetzungen

Die technischen Voraussetzungen werden in [Technologie](../technologie/zusammenspiel_der_tools.md) ausführlich beschrieben.

## Anleitung lesen oder OER erstellen

Zum Lesen dieser Anleitung benötigen Sie nur einen Browser. Die Anleitung ist unter <a href="https://quadriga-dk.github.io/QUADRIGA-OER-Manual/" class="external-link" target="_blank">https://quadriga-dk.github.io/QUADRIGA-OER-Manual/</a> verfügbar.

Wenn Sie eine eigene OER erstellen möchten, verwenden Sie die Vorlage <a href="https://github.com/quadriga-dk/Book_Template" class="external-link" target="_blank"><code>Book_Template</code></a>. Nutzen Sie dazu entweder die Template-Funktion "Use this template" in GitHub oder laden Sie sich den aktuellen Zustand bspw. als `.zip`-Datei herunter und fügen Sie ihn einem neuen Repositorium hinzu.

Passen Sie dann die Inhalte an. Insbesondere sollten Sie auf die Einstellungen in `_config.yml` und das Inhaltsverzeichnis in `_toc.yml` achten.

Wollen Sie GitHub Pages für die Veröffentlichung Ihres Jupyter Books nutzen, so müssen Sie einerseits die Funktionalität in den Einstellungen des Repositoriums anpassen und die passende GitHub Action in `.github/workflows/` auswählen und anpassen; im `Book_Template` ist dies beispielsweise `deploy-book-python-sparql-r.yml`. Zudem muss das Repositorium normalerweise öffentlich sein.

Eine Übersicht über alle Schritte von der Planung bis zur Veröffentlichung finden Sie in der <a href="https://github.com/quadriga-dk/QUADRIGA-OER-Manual/blob/main/reflexion_und_resümee/Checkliste_neue_OER.md" class="external-link" target="_blank">Checkliste für neue OER</a>.
