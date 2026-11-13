# QUADRIGA-OER: erstellen und gestalten mit Jupyter Book

````{margin}
```{admonition} Fragen oder Feedback
:class: frage-feedback

<a href="https://github.com/quadriga-dk/QUADRIGA-OER-Manual/issues/new?assignees=&labels=question&projects=&template=frage.yml" class="external-link" target="_blank">
    Stellen Sie eine Frage
</a> <br>
<a href="https://github.com/quadriga-dk/QUADRIGA-OER-Manual/issues/new?assignees=&labels=feedback&projects=&template=feedback.yml" class="external-link" target="_blank">
    Geben Sie uns Feedback
</a>

Mit Ihren Rückmeldungen können wir diese Anleitung gezielt verbessern.



```
````

`````{margin}
````{admonition} Zitierhinweis
:class: citation-information
```{literalinclude} /CITATION.bib
:language: bibtex
```
Schnaitter, H., Samoilova, E. & Islam, L. (2026). _QUADRIGA-OER: erstellen und gestalten mit Jupyter Book. QUADRIGA Open Educational Resources: Anleitung._ https://doi.org/10.5281/zenodo.18961415

````
`````

Diese **Anleitung** begleitet Sie bei der Erstellung von Open Educational Resources (OER) im Rahmen des <a href="https://www.quadriga-dk.de/" class="external-link" target="_blank">QUADRIGA-Projekts</a>. Sie beschreibt, wie QUADRIGA-OERs aufgebaut sind, welche didaktischen Empfehlungen gelten und wie Sie die Inhalte mit Markdown, Jupyter Notebooks und <a href="https://jupyterbook.org/v1/" class="external-link" target="_blank">Jupyter Book</a> {cite}`executable_books_community_2021_2561065` technisch umsetzen.

```{admonition} Anleitung und Vorlage sind getrennt
:class: hinweis

Diese Seite ist die **Anleitung**: Sie erklärt das Vorgehen und enthält Beispiele. Sie ist **kein Template** und sollte nicht als Ausgangspunkt für ein neues Buch kopiert werden.

Die **Vorlage** für neue QUADRIGA-OERs liegt separat auf GitHub: <a href="https://github.com/quadriga-dk/Book_Template" class="external-link" target="_blank">quadriga-dk/Book_Template</a> (<a href="https://quadriga-dk.github.io/Book_Template/" class="external-link" target="_blank">Demo</a>). Dort starten Sie mit der GitHub-Funktion *Use this template* oder mit einem ZIP-Download ein neues Repositorium und ersetzen die Beispielinhalte durch Ihre eigenen Inhalte.
```

## Anleitung und Vorlage im Überblick

| | Diese Anleitung | Book_Template |
|---|---|---|
| **Zweck** | Erklärt, wie QUADRIGA-OERs aufgebaut und mit Jupyter Book umgesetzt werden | Vorlage, aus der neue OER-Repositorien erstellt werden |
| **GitHub** | <a href="https://github.com/quadriga-dk/QUADRIGA-OER-Manual" class="external-link" target="_blank">quadriga-dk/QUADRIGA-OER-Manual</a> | <a href="https://github.com/quadriga-dk/Book_Template" class="external-link" target="_blank">quadriga-dk/Book_Template</a> |
| **Web-Version** | <a href="https://quadriga-dk.github.io/QUADRIGA-OER-Manual/" class="external-link" target="_blank">quadriga-dk.github.io/QUADRIGA-OER-Manual</a> | <a href="https://quadriga-dk.github.io/Book_Template/" class="external-link" target="_blank">quadriga-dk.github.io/Book_Template</a> |
| **Nutzung** | Lesen, nachschlagen und Empfehlungen auf die eigene OER anwenden | Mit *Use this template* oder als ZIP-Download kopieren und mit eigenen Inhalten füllen |

Die Anleitung zeigt die Möglichkeiten der Jupyter-Book-Plattform auf und fasst unsere Empfehlungen für die Entwicklung Ihrer OER zusammen. Gleichzeitig dient sie selbst als OER, mit der Sie die Gestaltung und Entwicklung von QUADRIGA-OERs erlernen können.

```{figure} /assets/intro/oer-creation-process.png
---
align: center
width: 70%
---
Aus dem Book_Template entstehen QUADRIGA-OERs, die mit Jupyter Book als Website gebaut werden.
```

## Für Lernende

Diese Anleitung ist für OER-Erstellende geschrieben. Wer eine fertige QUADRIGA-OER zum Lernen nutzt, braucht andere Hinweise: Wie man eine OER liest, in der Cloud ausführt oder lokal nutzt und wie man die Assessment-Angebote verwendet, steht in den **Lernhinweisen** (Learners Manual) unter <a href="https://quadriga-dk.github.io/QUADRIGA-Learners-Manual/" class="external-link" target="_blank">https://quadriga-dk.github.io/QUADRIGA-Learners-Manual/</a>. Verweisen Sie in Ihrer eigenen OER auf diese Seite, damit Lernende die passenden Nutzungshinweise finden.

## Zielgruppe

Diese Anleitung richtet sich an Personen, die QUADRIGA-OERs mit dem Book_Template erstellen möchten. Lernende, die eine fertige OER nutzen möchten, finden die passenden Hinweise in den separaten **Lernhinweisen** (Learners Manual, siehe Abschnitt *Für Lernende*).

## Aufbau dieser Anleitung

Die OER, die Sie mit dem Book_Template erstellen, folgen einem einheitlichen Aufbau. Im QUADRIGA-Projekt entwickeln wir Fallstudien, die auf datengetriebenen Forschungsaktivitäten basieren und spezifische Forschungsfragen zusammen mit den dazugehörigen Datensätzen und Methoden abbilden. Ihre OER sollte in empirische Schritte unterteilt werden, die:

- dem Datenlebenszyklus folgen,
- den strukturellen Rahmen für Lehrmaterialien bilden,
- den einzelnen Kapiteln im Jupyter Book entsprechen.

Diese Schritte sind im Book_Template bereits als Kapitelstruktur angelegt und werden dort mit den Inhalten Ihrer OER gefüllt.

```{mermaid}
:align: center
:caption: Aufbau einer QUADRIGA-OER aus sechs Schritten, wie er im Book_Template angelegt ist.

flowchart LR
    A["Einstieg"] --> B["Struktur und didaktisches Konzept"]
    B --> C["Technologie"]
    C --> D["Formatierungs- und<br/>Darstellungsmöglichkeiten"]
    D --> E["Lernstandskontrolle (Assessment)"]
    E --> F["Reflexion und Resümee"]
    F --> G["Abschluss"]
```

Die Anleitung selbst ist entlang derselben sechs Schritte gegliedert:

- Im **1. Schritt** führen wir in die OER ein, indem wir die Lernziele definieren und die technischen Voraussetzungen klären (siehe Kapitel {ref}`Einstieg<lernziele>`).
- Im **2. Schritt** stellen wir die inhaltliche Struktur einer QUADRIGA-OER vor und erläutern das zugrundeliegende didaktische Konzept (siehe Kapitel {ref}`Struktur und didaktisches Konzept<struktur:einleitung>`).
- Im **3. Schritt** beschäftigen wir uns mit der technischen Umsetzung und betrachten das Zusammenspiel der verschiedenen Tools und deren grafische Aufbereitung im Detail (siehe Kapitel {ref}`Technologie<technologie:einleitung>`).
- Im **4. Schritt** präsentieren wir zuerst allgemeine Hinweise zu Formatierungs- und Darstellungsmöglichkeiten und geben dann konkrete Vorgaben und Empfehlungen für QUADRIGA-OERs (siehe Kapitel {ref}`Formatierung<formatierung:einleitung>`).
- Im **5. Schritt** widmen wir uns der Lernstandskontrolle, indem wir die Rolle des Assessments in QUADRIGA-OERs erläutern und dessen konkrete Umsetzungsmöglichkeiten aufzeigen (siehe Kapitel {ref}`Lernstandskontrolle (Assessment)<assessment:einleitung>`).
- Im **6. Schritt** schließen wir die OER inhaltlich mit einem Abschlussassessment ab, fassen die wichtigsten Punkte zusammen und geben weiterführende Hinweise (siehe Kapitel {ref}`Reflexion und Resümee<reflexion>`).

Der Abschluss rundet die OER ab: Er bietet Raum für Fragen und Feedback, enthält das Literaturverzeichnis, stellt die Autor:innen vor und liefert Informationen zu QUADRIGA sowie das Impressum (siehe Kapitel {ref}`Abschluss<fragen_feedback>`).

**Literatur**

```{bibliography}
:filter: docname in docnames
```
