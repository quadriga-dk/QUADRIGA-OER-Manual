# Lokale Ausführung des Jupyter Books

Die Ausführung des Buchs in der lokalen Umgebung bietet Ihnen maximale Kontrolle: Sie können offline arbeiten, auf alle Dateien zugreifen, Ihre eigenen Daten integrieren und das Material frei anpassen. Dies erfordert jedoch die Einrichtung der korrekten Umgebung (Python, R oder SPARQL je nach Kapitel).

```{admonition} Welches Buch ist gemeint?
:class: hinweis

Wenn in diesem Kapitel von „diesem Buch“ die Rede ist, ist damit die jeweilige OER gemeint – also das Jupyter Book, das Sie mit dem <a href="https://github.com/quadriga-dk/Book_Template" class="external-link" target="_blank"><code>Book_Template</code></a> erstellen. Die Dateien dafür stammen aus dem `Book_Template`. Möchten Sie stattdessen diese Anleitung lokal nachvollziehen oder zu ihr beitragen, nutzen Sie das <a href="https://github.com/quadriga-dk/QUADRIGA-OER-Manual" class="external-link" target="_blank">Repositorium der Anleitung</a>.
```


 ````{admonition} Hinweis
:class: hinweis
Bevor Sie beginnen, stellen Sie bitte sicher, dass Python auf Ihrem Computer installiert ist. Falls Python fehlt oder veraltet ist, folgen Sie bitte der Installationsanleitung [hier](python).
 ````

## Repository herunterladen

Sie benötigen die Notebooks und Ressourcen aus dem Repository Ihres Buchs. Für Ihre eigene OER ist damit das Repositorium gemeint, das Sie aus dem `Book_Template` erstellt haben; für diese Anleitung ist es das Repositorium der Anleitung. Es gibt zwei Möglichkeiten, diese Dateien zu erhalten:

1. **Download als ZIP**
    - Für Ihre eigene OER: Legen Sie zunächst mit der GitHub-Funktion *Use this template* im <a href="https://github.com/quadriga-dk/Book_Template" class="external-link" target="_blank"><code>Book_Template</code></a> ein neues Repositorium an. Gehen Sie dann in diesem Repositorium auf Code → Download ZIP.
    - Für diese Anleitung: Gehen Sie im <a href="https://github.com/quadriga-dk/QUADRIGA-OER-Manual" class="external-link" target="_blank">Repositorium der Anleitung</a> auf Code → Download ZIP.
    - Entpacken Sie die ZIP-Datei auf Ihrem Computer.

2. **Oder über Git clone** (falls Sie Git bereits installiert haben)
    - Für Ihre eigene OER: Klonen Sie das Repositorium, das Sie aus dem `Book_Template` erstellt haben. Wie das funktioniert, lesen Sie im Abschnitt [Git](git).
    - Für diese Anleitung:
      ```bash
      git clone https://github.com/quadriga-dk/QUADRIGA-OER-Manual
      ```


## Lokale Umgebung erstellen

Im heruntergeladenen Ordner sollten Sie eine lokale Umgebung mit allen benötigten Abhängigkeiten einrichten (siehe `requirements.txt`). Nur so ist sichergestellt, dass die Notebooks korrekt laufen.

Weitere Informationen finden Sie im Abschnitt [Einrichtung der lokalen Entwicklungsumgebung](jupyter_book) für schrittweise Anweisungen, und Sie haben die lokale Version des Jupyter Books bereit!

## Jupyter Notebooks ausführen

Um die Jupyter Notebooks (.ipynb-Dateien) zu öffnen und auszuführen, navigieren Sie in den Buchordner und starten Jupyter über das Terminal:

```bash
jupyter lab
```
oder

```bash
jupyter notebook
```

Dies startet einen lokalen Server und öffnet ein Browserfenster, in dem Sie die Notebooks ausführen oder bearbeiten können.

Um den Server zu stoppen, kehren Sie zum Terminal zurück, in dem er läuft, und drücken `Strg + C`.

## Spezialfälle (andere Programmiersprachen)

Einige Kapitel verwenden möglicherweise `R` oder `SPARQL`. In diesem Fall müssen Sie zusätzliche Kernel installieren.

### R

1. Installieren Sie <a href="https://cran.r-project.org/" target="_blank" class="external-link">R</a> und <a href="https://posit.co/download/rstudio-desktop/" target="_blank" class="external-link">RStudio</a>.
2. Installieren Sie aus R oder RStudio heraus das IRkernel-Paket:
   ```r
   install.packages("IRkernel")
   IRkernel::installspec(user = FALSE)
   ```

Dies registriert R als Jupyter-Kernel, sodass Sie R-Notebooks innerhalb von JupyterLab oder Jupyter Notebook ausführen können.

### SPARQL

Um SPARQL-Abfragen in Jupyter auszuführen, benötigen Sie den SPARQL-Kernel.

1. Stellen Sie sicher, dass Jupyter installiert ist.
2. Installieren Sie den Kernel mit:
   ```bash
   jupyter sparqlkernel install --user
   ```

Danach können Sie SPARQL als Kernel auswählen, wenn Sie relevante Notebooks öffnen.

Wenn Sie mehr über Kernel erfahren möchten, lesen Sie den Abschnitt [Jupyter Kernels](jupyter_kernel).

## Alternative: Einzelnes Notebook herunterladen

Wenn Sie nur ein Kapitel ausprobieren möchten, ohne das vollständige Repository einzurichten:

1. Laden Sie die .ipynb-Datei direkt aus dem Buch herunter (rechts oben → Download-Symbol).
2. Öffnen Sie sie in JupyterLab, Jupyter Notebook oder RStudio.

````{admonition} Achtung!
:class: caution
Möglicherweise benötigen Sie zugehörige Datensätze oder Unterstützungsdateien – diese Einrichtung funktioniert am besten nur für eigenständige, in sich geschlossene Notebooks.
````

In den meisten Fällen ist das Arbeiten mit dem vollständigen Repository der einfachste und verlässlichste Weg, um die eigene OER bzw. diese Anleitung zu erkunden. Für einen ersten Einstieg können einzelne Notebooks dennoch hilfreich sein.

````{admonition} Zusätzliche Materialien
:class: seealso
* [Git für Versionsverwaltung verwenden](git)
* [Python](python)  
* [Jupyter Books lokal ausführen](jupyter_book)
* [Editoren für Jupyter Notebooks](editor)
````