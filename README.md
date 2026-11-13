# QUADRIGA-OER: erstellen und gestalten mit Jupyter Book – QUADRIGA Open Educational Resources: Anleitung

[![DOI](https://zenodo.org/badge/1171691941.svg)](https://doi.org/10.5281/zenodo.18961415)

Launch the latest version in Binder: [![Binder](https://mybinder.org/badge_logo.svg)](https://mybinder.org/v2/gh/quadriga-dk/QUADRIGA-OER-Manual/main)

Dieses Repositorium enthält die **Anleitung** für <a href="https://www.quadriga-dk.de" class="external-link" target="_blank">QUADRIGA</a> OERs, die mit <a href="https://jupyterbook.org" target="_blank" class="external-link">Jupyter Book</a> erstellt werden. Die Anleitung erklärt, wie QUADRIGA-OERs aufgebaut sind, welche didaktischen und technischen Konzepte dahinterstehen und wie Sie Inhalte formatieren, prüfen und veröffentlichen.

Die Anleitung ist selbst **kein Template**. Wenn Sie eine eigene OER erstellen möchten, verwenden Sie die Vorlage <a href="https://github.com/quadriga-dk/Book_Template" class="external-link" target="_blank"><code>Book_Template</code></a>.

## Anleitung und Vorlage

| | Zweck | Repository | Website |
|---|---|---|---|
| **Anleitung** (dieses Repositorium) | Erklärt, wie QUADRIGA-OERs mit Jupyter Book erstellt und gestaltet werden. | <a href="https://github.com/quadriga-dk/QUADRIGA-OER-Manual" class="external-link" target="_blank">quadriga-dk/QUADRIGA-OER-Manual</a> | <a href="https://quadriga-dk.github.io/QUADRIGA-OER-Manual/" class="external-link" target="_blank">quadriga-dk.github.io/QUADRIGA-OER-Manual</a> |
| **Vorlage** (`Book_Template`) | Dient als Ausgangspunkt für eine neue OER und wird mit eigenen Inhalten gefüllt. | <a href="https://github.com/quadriga-dk/Book_Template" class="external-link" target="_blank">quadriga-dk/Book_Template</a> | <a href="https://quadriga-dk.github.io/Book_Template/" class="external-link" target="_blank">quadriga-dk.github.io/Book_Template</a> |

Die Anleitung können Sie direkt im Browser lesen: <a href="https://quadriga-dk.github.io/QUADRIGA-OER-Manual/" class="external-link" target="_blank">https://quadriga-dk.github.io/QUADRIGA-OER-Manual/</a>. Die Vorlage können Sie sich in der Demo-Version ansehen: <a href="https://quadriga-dk.github.io/Book_Template/" class="external-link" target="_blank">https://quadriga-dk.github.io/Book_Template/</a>.

## Verwandte Repositorien

- **Anleitung** (dieses Repositorium): Erklärt, wie QUADRIGA-OERs mit Jupyter Book erstellt und gestaltet werden – <a href="https://quadriga-dk.github.io/QUADRIGA-OER-Manual/" class="external-link" target="_blank">https://quadriga-dk.github.io/QUADRIGA-OER-Manual/</a>
- **Lernhinweise (Learners Manual):** Richtet sich an Lernende und beschreibt, wie eine QUADRIGA-OER gelesen, in der Cloud ausgeführt oder lokal genutzt wird – <a href="https://quadriga-dk.github.io/QUADRIGA-Learners-Manual/" class="external-link" target="_blank">https://quadriga-dk.github.io/QUADRIGA-Learners-Manual/</a> (<a href="https://github.com/quadriga-dk/QUADRIGA-Learners-Manual" class="external-link" target="_blank">quadriga-dk/QUADRIGA-Learners-Manual</a>)
- **Vorlage (`Book_Template`):** Ausgangspunkt für eine neue OER – <a href="https://github.com/quadriga-dk/Book_Template" class="external-link" target="_blank">quadriga-dk/Book_Template</a> (<a href="https://quadriga-dk.github.io/Book_Template/" class="external-link" target="_blank">Demo</a>)

## Neue OER erstellen

1. **`Book_Template` als neues Repositorium anlegen.** Erstellen Sie ein neues Repositorium mit dem Namen Ihrer OER – innerhalb des QUADRIGA-Projekts in der GitHub-Organisation `quadriga-dk`, andernfalls in Ihrem eigenen GitHub-Account. Nutzen Sie dazu die GitHub-Funktion "Use this template" im <a href="https://github.com/quadriga-dk/Book_Template" class="external-link" target="_blank"><code>Book_Template</code></a> oder laden Sie die Vorlage als `.zip`-Datei herunter und legen Sie die Inhalte in einem neuen Repositorium ab.
2. **`_config.yml`, `_toc.yml` und den GitHub-Workflow anpassen.** Passen Sie die Metadaten in `_config.yml` und das Inhaltsverzeichnis in `_toc.yml` an Ihre OER an. Wählen Sie in `.github/workflows/` die passende GitHub Action aus und passen Sie sie an; im `Book_Template` ist dies beispielsweise `deploy-book-python-sparql-r.yml`.
3. **Beispielinhalte ersetzen.** Ersetzen Sie die Beispielinhalte der Vorlage durch Ihre eigene Fallstudie, Ihre Kapitel und Ihre Materialien. Achten Sie darauf, dass Ihr neues Buch keine direkte Verbindung zur Vorlage mehr hat; Änderungen an `Book_Template` müssen Sie gegebenenfalls "von Hand" in Ihre OER übernehmen.
4. **Checkliste nutzen.** Arbeiten Sie die <a href="https://github.com/quadriga-dk/QUADRIGA-OER-Manual/blob/main/reflexion_und_resümee/Checkliste_neue_OER.md" class="external-link" target="_blank">Checkliste für neue OER</a> durch. Sie fasst alle Schritte von der Planung bis zur Veröffentlichung zusammen.

Übernehmen Sie Änderungen am Styling und Layout der Vorlage auch in Ihrer OER. Bei wichtigen Änderungen kann ein Pull-Request an Ihre Bücher durch die (`Book_Template`-)Autor:innen gestellt werden.

Die Kapitel dieser Anleitung führen Sie durch die einzelnen Schritte: von den Lernzielen und technischen Voraussetzungen über die Struktur und das didaktische Konzept bis hin zu Formatierung, Assessment und Veröffentlichung. Nutzen Sie die Anleitung parallel zur Arbeit mit dem `Book_Template`.
