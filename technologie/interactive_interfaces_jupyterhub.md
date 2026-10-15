# Interaktive Rechenumgebungen mit JupyterHub

JupyterHub ist ein Server, auf dem viele Nutzer:innen gleichzeitig mit Jupyter-Notebooks arbeiten können. Jede Person meldet sich an und erhält ihre eigene Arbeitsumgebung im Browser. Über einen Launch-Button in Ihrem Jupyter Book öffnen Sie das passende Notebook direkt auf diesem Server. JupyterHub wird häufig von Universitäten und Organisationen betrieben.

Im Gegensatz zu Google Colab und Binder gehört JupyterHub nicht zu einem öffentlichen Dienst. Sie benötigen einen JupyterHub, den Ihre Organisation betreibt, oder einen eigenen Server. Dafür bestimmen Sie selbst, wer Zugang hat und welche Software und Ressourcen zur Verfügung stehen.


## Wie JupyterHub funktioniert

**1. Anmeldung**
Nutzer:innen klicken im Buch auf "Launch (🚀) → JupyterHub" und melden sich auf dem Hub an.

**2. Persönliche Umgebung**
JupyterHub startet für jede Person eine eigene Jupyter-Sitzung auf dem Server.

**3. Dateien laden**
Die Dateien Ihres Buches werden automatisch aus Ihrem Git-Repository in Ihre Umgebung kopiert.

**4. Interaktive Sitzung**
Das Notebook öffnet sich im Browser und kann ausgeführt werden. Alles läuft auf dem Server, nicht auf dem eigenen Rechner.

```{admonition} Wichtig zu wissen
:class: keypoint
Der Launch-Button kopiert nur die Dateien Ihres Buches in Ihre Umgebung. Die Python-Pakete, die Ihre Notebooks brauchen, müssen auf dem JupyterHub bereits vorhanden sein. Anders als bei Binder werden `requirements.txt` oder `Dockerfile` nicht automatisch ausgeführt.

Geben Sie der IT-Administration deshalb eine Liste der benötigten Pakete, am besten Ihre `requirements.txt`. Leser:innen müssen dann nichts installieren.
```


## JupyterHub bereitstellen

Ein JupyterHub muss von jemandem betrieben werden. Dafür gibt es zwei Wege.

### Option 1: Den JupyterHub Ihrer Organisation nutzen

Das ist für die meisten der einfachste Weg. Viele Hochschulen und Forschungseinrichtungen betreiben bereits einen JupyterHub. Fragen Sie bei Ihrem IT- oder Rechenzentrum nach folgenden Punkten:

- Wie lautet die Adresse (URL) des JupyterHub?
- Wer darf sich anmelden? Gibt es Zugangsbeschränkungen, zum Beispiel nur im Hochschulnetz oder über VPN?
- Ist `nbgitpuller` installiert? Ohne diese Erweiterung funktioniert der Launch-Button nicht.
- Welche Python-Pakete und welche Umgebung stehen zur Verfügung? Können fehlende Pakete nachinstalliert werden?
- Wie viel Arbeitsspeicher (RAM) und Speicherplatz bekommt jede Person?
- Werden gespeicherte Dateien dauerhaft aufbewahrt?

### Option 2: Einen eigenen JupyterHub aufbauen

Dafür brauchen Sie in der Regel:

- einen Server oder eine virtuelle Maschine mit Administratorrechten,
- Grundkenntnisse in der Arbeit mit der Kommandozeile,
- eine Adresse, unter der die Nutzer:innen den Server erreichen,
- eine verschlüsselte Verbindung (HTTPS),
- eine Möglichkeit, Benutzerkonten zu verwalten.

Für kleinere Gruppen auf einem einzelnen Server gibt es "The Littlest JupyterHub". Für größere Gruppen setzen Organisationen oft eine Kubernetes-Variante ein ("Zero to JupyterHub").

```{admonition} Hinweis für Einsteiger:innen
:class: caution
Der Aufbau eines JupyterHub ist eine Aufgabe für IT-Administrator:innen. Installieren Sie ihn nicht auf Ihrem normalen Arbeitsrechner. Wenn Sie keine Erfahrung mit Servern haben, sprechen Sie zuerst mit Ihrer IT-Abteilung. Die Schritt-für-Schritt-Anleitungen finden Sie in der offiziellen Dokumentation (siehe "Zusätzliche Materialien" am Ende des Kapitels).
```


## Technische Konfiguration

Wenn Sie die Adresse eines JupyterHub haben, aktivieren Sie den Launch-Button in der Datei `_config.yml`. Fügen Sie folgende Zeilen hinzu:

```yaml
repository:
  url: https://github.com/your-username/your-repo  # GitHub-Adresse des Projekts
  branch: main  # Branch mit den Quelldateien des Buches
  path_to_book: ""  # Unterordner des Buches; leer lassen, wenn das Buch im Hauptordner liegt

launch_buttons:
  notebook_interface: jupyterlab  # Oberfläche: jupyterlab oder classic
  jupyterhub_url: https://your-hub-address  # Adresse Ihres JupyterHub
```

Die wichtigsten Einstellungen:

- `url`: GitHub-Adresse des Repositories mit den Quelldateien Ihres Buches.
- `branch`: Branch mit diesen Quelldateien, zum Beispiel `main`.
- `path_to_book`: Unterordner, in dem das Buch liegt. Liegt es im Hauptordner, bleibt der Wert leer.
- `jupyterhub_url`: Adresse Ihres JupyterHub, ohne zusätzlichen Pfad.

Wenn Sie bereits Colab und Binder verwenden, ergänzen Sie nur die neue Zeile im vorhandenen Abschnitt `launch_buttons`:

```yaml
launch_buttons:
  notebook_interface: jupyterlab
  colab_url: https://colab.research.google.com
  binderhub_url: https://mybinder.org
  jupyterhub_url: https://your-hub-address
```

```{admonition} Tipp
:class: keypoint
Legen Sie keinen zweiten Abschnitt `launch_buttons` oder `repository` an. Ergänzen Sie immer die vorhandenen Abschnitte. Erstellen Sie das Buch danach neu, zum Beispiel mit `jupyter-book build .`. Der Button erscheint nur auf Seiten, die aus Notebooks erstellt wurden.
```


## Häufige Herausforderungen

**Zugang und Anmeldung**: Nur Personen mit einem Konto auf dem Hub können Notebooks starten. Prüfen Sie vorab, wer Zugang erhält und ob ein VPN oder das Hochschulnetz nötig ist.

**Fehlende Pakete**: Der Hub nutzt nicht automatisch Ihre `requirements.txt`. Wenn ein Paket fehlt, geben Sie der IT-Administration die Liste der benötigten Pakete. Fragen Sie außerdem nach, ob Sie Pakete selbst im Notebook installieren dürfen (zum Beispiel mit `!pip install paketname`) und ob diese nach dem Ende der Sitzung noch vorhanden sind.

**Fehler beim Öffnen des Notebooks**: Erscheint nach dem Klick auf den Button eine Fehlerseite, ist oft `nbgitpuller` nicht installiert. Prüfen Sie außerdem Branch und `path_to_book` in der `_config.yml`.

**Begrenzte Ressourcen**: Alle Nutzer:innen teilen sich die Hardware des Servers. Wenn ein Notebook sehr viel Arbeitsspeicher braucht, kann die Sitzung beendet werden. Planen Sie bei Workshops mit vielen Teilnehmenden Zeit für anspruchsvolle Berechnungen ein.

**Änderungen gehen nicht ins Repository zurück**: Sie arbeiten mit einer persönlichen Kopie der Dateien. Änderungen in dieser Kopie werden nicht automatisch an GitHub übertragen.

```{admonition} Bewährte Praktiken
:class: keypoint
Speichern Sie Ihre Arbeit regelmäßig und laden Sie wichtige Ergebnisse zusätzlich auf Ihren eigenen Rechner herunter. Klären Sie mit der Administration, wie lange Dateien auf dem Hub aufbewahrt werden.
```


## Vergleich: Colab, Binder und JupyterHub

| Merkmal | Google Colab | Binder | JupyterHub |
|---------|-------------|---------|------------|
| **Betreiber** | Google | Öffentlicher Dienst (mybinder.org) oder eigener BinderHub | Ihre Organisation oder Sie selbst |
| **Umgebungskontrolle** | Googles vorinstallierte Pakete; zusätzliche Pakete manuell installieren | Baut Ihre Umgebung aus Konfigurationsdateien nach | Festgelegt von der Administration; Pakete werden auf dem Server installiert |
| **Dateizugriff** | Öffnet einzelne Notebooks; Dateien manuell hochladen | Zugriff auf die gesamte Repository-Struktur | Dateien des Buches werden automatisch in Ihre Umgebung kopiert |
| **Persistenz** | Speichern in Google Drive möglich | Temporäre Sitzungen; Arbeit manuell herunterladen | Je nach Konfiguration; dauerhafter Speicherplatz möglich |
| **Datenschutz** | Notebooks liegen in Google Drive; der Code läuft auf Google-Servern und ist an Ihr Google-Konto gebunden | Öffentlicher Dienst: nicht für personenbezogene oder vertrauliche Daten geeignet; private Dateien sind nicht zugänglich | Die Organisation bestimmt, wo die Daten liegen und wer darauf zugreifen darf |
| **Setup-Aufwand** | Minimal; funktioniert sofort | Konfigurationsdateien im Repository nötig | Hub muss bereitgestellt und eingerichtet werden |
| **Anmeldung** | Google-Account | Kein Account nötig | Konto auf dem Hub nötig |
| **Ressourcen** | Mehr Rechenleistung, GPU-Zugriff möglich | Begrenzt | Abhängig von der Hardware des Servers |

```{admonition} Datenschutz beachten
:class: caution
**Colab:** Notebooks werden in Google Drive gespeichert, und der Code läuft auf Google-Servern. Verwenden Sie keine vertraulichen oder personenbezogenen Daten, ohne vorher die Regeln Ihrer Einrichtung zu prüfen.

**Binder:** mybinder.org ist ein öffentlicher Dienst. Geben Sie dort niemals Passwörter oder sensible Daten ein. Jeder Start wird öffentlich protokolliert (Repository und Zeitpunkt, aber keine Angaben zur Person), es gibt also keinen privaten Start.

**JupyterHub:** Die Organisation, die den Hub betreibt, ist für den Schutz der Daten verantwortlich. Fragen Sie dort nach, welche Daten gespeichert werden und wie lange.

Für Lehrmaterialien mit öffentlichen Daten sind alle drei Optionen geeignet. Bei Interviews, Umfragen oder anderen personenbezogenen Daten ist ein Hub Ihrer Organisation meist die bessere Wahl.
```

JupyterHub eignet sich besonders, wenn eine Organisation Workshops oder Kurse anbietet und die Umgebung selbst kontrollieren möchte, zum Beispiel aus Gründen des Datenschutzes oder wegen größerer Rechenressourcen.


```{admonition} Zusätzliche Materialien
:class: seealso
Für detaillierte Informationen zur Konfiguration von Launch-Buttons empfehlen wir die offizielle <a href="https://jupyterbook.org/v1/interactive/launchbuttons.html" class="external-link" target="_blank">Jupyter Book Dokumentation zu Launch Buttons</a>.

Eine Einführung in JupyterHub finden Sie in der <a href="https://jupyterhub.readthedocs.io/" class="external-link" target="_blank">offiziellen JupyterHub Dokumentation</a>. Für einen einfachen Hub auf einem einzelnen Server empfehlen wir <a href="https://tljh.jupyter.org/" class="external-link" target="_blank">The Littlest JupyterHub</a>. Für größere Installationen mit Kubernetes gibt es <a href="https://z2jh.jupyter.org/" class="external-link" target="_blank">Zero to JupyterHub with Kubernetes</a>.

Informationen zur Erweiterung, die die Buchdateien in die Umgebung kopiert, finden Sie in der <a href="https://nbgitpuller.readthedocs.io/" class="external-link" target="_blank">nbgitpuller Dokumentation</a>.
```
