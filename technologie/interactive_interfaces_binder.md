# Interaktive Rechenumgebungen mit Binder

Binder erstellt reproduzierbare, interaktive Rechenumgebungen aus Git-Repositories. Im Gegensatz zu Google Colab repliziert Binder exakt die im Repository definierte Umgebung, inklusive aller Pakete und Versionen. Über "Launch (🚀) → Binder" starten Leser:innen eine Live-Version der Notebooks mit allen Abhängigkeiten. Für Projekte ohne hohe CPU- oder RAM-Anforderungen kann der öffentliche BinderHub genutzt werden.

## Wie Binder Ihr Repository verarbeitet

**1. Analyse des Repositories**
Binder untersucht beim Start der Umgebung das GitHub-Repository, das in Ihrer `_config.yml` hinterlegt ist.

**2. Erstellung der Umgebung**
Basierend auf den gefundenen Konfigurationsdateien (z. B. requirements.txt, environment.yml oder Dockerfile) wird ein Docker-Image gebaut. Dieser Build dauert beim ersten Mal einige Minuten und wird zwischengespeichert.

**3. Start der Umgebung**
Leser:innen erhalten Zugriff auf eine vollständige Jupyter-Oberfläche im Browser – inklusive aller Projektdateien und Abhängigkeiten.


## Technische Konfiguration
Um den Binder-Launch-Button zu aktivieren, stellen Sie sicher, dass die folgenden Zeilen in Ihrer `_config.yml`-Datei enthalten sind:

```yaml
repository:
  url: https://github.com/your-username/your-repo  # GitHub-Adresse des Projekts
  branch: main  # Standardbranch, z. B. "main" oder "master"

launch_buttons:
  notebook_interface: jupyterlab  # Oberfläche: jupyterlab oder classic
  binderhub_url: https://mybinder.org
```


## Erforderliche Dateien

Binder sucht nach Konfigurationsdateien im Stammverzeichnis Ihres Repositories. Sie benötigen nur die Dateien, die für Ihr Projekt relevant sind:

**`requirements.txt`**  
 Enthält eine Liste der Python-Pakete und deren Versionen, die für die Umgebung erforderlich sind.  

 ````{admonition} Beispiel: requirements.txt
:class: hinweis, dropdown
```
jupyter-book==1.0.4
jupyterquiz==2.8.*
matplotlib
numpy
````

**`postBuild`**   
 Führt benutzerdefinierte Befehle aus, die nach dem Erstellen der Umgebung ausgeführt werden sollen.  

 ````{admonition} Beispiel: postBuild
:class: hinweis, dropdown
```
jupyter sparqlkernel install --user
````

**`install.R`**  
Installiert die benötigten R-Pakete und richtet den R-Kernel ein.  

````{admonition} Beispiel: install.R
:class: hinweis, dropdown
```
install.packages("ggplot2")
install.packages("dplyr")
install.packages("SPARQL")
IRkernel::installspec(user = FALSE)
````

### Erweiterte Konfiguration mit Docker

Für komplexe Umgebungen können Sie ein `Dockerfile` verwenden. Binder priorisiert dies gegenüber anderen Konfigurationsdateien:

````{admonition} Beispiel: Dockerfile
:class: hinweis, dropdown
```dockerfile
# Variablen für Container-Besitzer und Basis-Image
ARG OWNER=jupyter
ARG BASE_CONTAINER=$OWNER/minimal-notebook
FROM $BASE_CONTAINER

# Shell-Konfiguration
SHELL ["/bin/bash", "-o", "pipefail", "-c"]

USER root

# System-Pakete installieren: 
# Hier können Sie weitere System-Pakete hinzufügen (z.B. curl, build-essential)
RUN apt-get update --yes && \
    apt-get install --yes --no-install-recommends \
    fonts-dejavu \
    gfortran \
    gcc && \
    apt-get clean && rm -rf /var/lib/apt/lists/*

USER ${NB_UID}

# R und R-Pakete installieren: 
# Nach Bedarf hinzufügen oder entfernen (z.B. 'r-ggplot2', 'r-dplyr')
RUN mamba install --quiet --yes \
    'r-base' \
    'r-tidyverse' \
    'r-irkernel' && \
    mamba clean --all -f -y && \
    fix-permissions "${CONDA_DIR}"

# Repository kopieren
USER root
COPY . ${HOME}
RUN chown -R ${NB_USER} ${HOME}
USER ${NB_UID}

# Python-Pakete installieren: 
# Zum Hinzufügen oder Entfernen von Bibliotheken bearbeiten Sie die requirements.txt-Datei
RUN pip install -r requirements.txt

# Zusätzliche Jupyter-Kernel installieren (z.B. SPARQL)
RUN jupyter sparqlkernel install --user

WORKDIR "${HOME}"
```
````

```{admonition} Was sollten Sie verwenden?
:class: caution

**Verwenden Sie Docker, wenn:**
Komplexe Systeminstallationen erforderlich sind, Sie mehrere Programmiersprachen mischen, spezifische Versionen von Systembibliotheken benötigen oder vollständige Kontrolle über die Umgebung wünschen.

**Verwenden Sie einfache Konfigurationsdateien, wenn:**
Sie Standard-Python- oder R-Pakete nutzen, schnellere Build-Zeiten benötigen oder eine einfachere Wartung bevorzugen.
```

## Häufige Herausforderungen beim Bereitstellen

**Umgebungs-Build-Zeit**: Binder muss Ihre Umgebung beim ersten Mal erstellen und dabei alle Pakete aus Ihren Konfigurationsdateien installieren. Dies kann insbesondere bei R-Paketen zeitaufwendig sein. Testen Sie den Build vor der Veröffentlichung und rechnen Sie beim ersten Start mit Wartezeit für Ihre Leser:innen.

**Temporäre Sitzungen**: Binder-Sitzungen sind zeitlich begrenzt und werden nach einer Phase der Inaktivität beendet. Änderungen werden nicht in Ihr Repository zurückgespeichert. Weisen Sie Lernende in Ihrer OER darauf hin, Arbeitsergebnisse rechtzeitig herunterzuladen (siehe Abschnitt *Nutzung durch Lernende*).

```{admonition} Bewährte Praktiken
:class: keypoint
Beschränken Sie sich auf notwendige Pakete in Ihren Konfigurationsdateien. Verwenden Sie spezifische Versionsnummern für Reproduzierbarkeit und testen Sie Ihre Umgebung lokal vor der Bereitstellung.
```

## Nutzung durch Lernende

Wie Lernende ein Notebook über den Launch-Button öffnen, mit den Sitzungsgrenzen umgehen und ihre Ergebnisse sichern, steht im Learners Manual: <a href="https://quadriga-dk.github.io/QUADRIGA-Learners-Manual/nutzung/modi/cloud.html" class="external-link" target="_blank">Cloud-Ausführung im Learners Manual</a>. Verweisen Sie in Ihrer OER auf diese Seite, statt die Hinweise im Buch selbst zu wiederholen.

## Vergleich: Colab vs. Binder

| Merkmal | Google Colab | Binder |
|---------|-------------|---------|
| **Umgebungskontrolle** | Nutzt Googles vorinstallierte Pakete; zusätzliche Pakete erfordern manuelle Installation | Erstellt Ihre exakte Umgebung aus Konfigurationsdateien nach |
| **Dateizugriff** | Öffnet einzelne Notebooks; erfordert manuelles Hochladen zusätzlicher Dateien | Bietet Zugriff auf die gesamte Repository-Struktur und Dateien |
| **Persistenz** | Kann in Google Drive speichern; integriert in Google-Ökosystem | Temporäre Sessions; Arbeit muss manuell heruntergeladen werden |
| **Setup-Anforderungen** | Minimaler Setup; funktioniert sofort mit jedem Notebook | Erfordert ordnungsgemäße Konfigurationsdateien und Umgebungsspezifikation |
| **Ressourcenverfügbarkeit** | Bietet GPU-Zugriff und generell mehr Rechenressourcen | Begrenzte Ressourcen; besser geeignet für Bildungsinhalte und Demos |
| **Nutzererfahrung** | Vertraute Google-Oberfläche; erfordert Google-Account | Native Jupyter-Oberfläche; kein Account erforderlich |

Binder eignet sich besonders gut für pädagogische Jupyter Books, bei denen Sie eine vollständige, reproduzierbare Umgebung bereitstellen möchten, die Ihrem lokalen Entwicklungssetup entspricht.


```{admonition} Zusätzliche Materialien
:class: seealso
Für detaillierte Informationen zur Konfiguration von Launch-Buttons in Jupyter Book empfehlen wir die offizielle <a href="https://jupyterbook.org/v1/interactive/launchbuttons.html" class="external-link" target="_blank">Jupyter Book Dokumentation zu Launch Buttons</a>. 

Für umfassende Informationen zu Binder-Konfigurationen und erweiterten Setup-Optionen konsultieren Sie die <a href="https://mybinder.readthedocs.io/en/latest/" class="external-link" target="_blank">offizielle Binder Dokumentation</a>. Praktische Beispiele und Templates für verschiedene Umgebungen finden Sie in den <a href="https://github.com/binder-examples" class="external-link" target="_blank">Binder Examples Repository</a>.

```