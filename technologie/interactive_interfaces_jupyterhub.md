# Interaktive Rechenumgebungen mit JupyterHub

<a href="https://jupyter.org/hub" class="external-link" target="_blank">JupyterHub</a> ist ein Server, auf dem viele Nutzer:innen gleichzeitig mit Jupyter-Notebooks arbeiten können. Mit JupyterHub können Sie einen Online-Dienst betreiben, der jeder Person einen eigenen Jupyter-Server zur Verfügung stellt. Die Arbeitsumgebung legen Sie selbst fest. Sie können außerdem die Rechenleistung und Hardware bereitstellen, die Ihre Nutzer:innen brauchen. Über eine Anmeldung steuern Sie, wer diese Ressourcen nutzen darf.

JupyterHub eignet sich, wenn Sie Kurse oder Workshops anbieten, die Umgebung selbst kontrollieren möchten oder mehr Rechenleistung benötigen, als öffentliche Dienste bieten. Ähnlich wie bei Binder können Sie in Ihrem Jupyter Book Launch-Buttons einbauen. Ein Klick darauf öffnet die jeweilige Seite als interaktives Notebook auf Ihrem JupyterHub. Die Leser:innen können den Code dort direkt ausprobieren.

```{admonition} Hinweis
:class: hinweis
Im Gegensatz zu Google Colab und Binder ist JupyterHub kein öffentlicher Dienst. Sie benötigen einen JupyterHub, den Ihre Organisation betreibt, oder einen eigenen Server.
```


## JupyterHub im Jupyter Book aktivieren

Haben Sie die Adresse eines JupyterHub, aktivieren Sie den Launch-Button in der Datei `_config.yml`:

```yaml
repository:
  url: https://github.com/your-username/your-repo  # GitHub-Adresse des Projekts
  branch: main  # Branch mit den Quelldateien des Buches
  path_to_book: ""  # Unterordner des Buches; leer lassen, wenn das Buch im Hauptordner liegt

launch_buttons:
  notebook_interface: jupyterlab  # Oberfläche: jupyterlab oder classic
  jupyterhub_url: "https://your-hub-address"  # Adresse Ihres JupyterHub, z. B. https://datahub.berkeley.edu
```

Wenn Sie bereits Colab oder Binder verwenden, ergänzen Sie `jupyterhub_url` im vorhandenen Abschnitt `launch_buttons` und erstellen Sie das Buch danach neu.


## Wie JupyterHub funktioniert

**1. Anmeldung**
Nutzer:innen klicken im Buch auf "Launch (🚀) → JupyterHub" und melden sich auf dem Hub an.

**2. Persönliche Umgebung**
JupyterHub startet für jede Person eine eigene Jupyter-Sitzung auf dem Server.

**3. Dateien laden**
Die Dateien Ihres Buches werden automatisch aus Ihrem Git-Repository in Ihre Umgebung kopiert.

**4. Interaktive Sitzung**
Das Notebook öffnet sich im Browser und kann ausgeführt werden. Alles läuft auf dem Server, nicht auf dem eigenen Rechner.


## JupyterHub bereitstellen

Ein JupyterHub muss von jemandem betrieben werden. Dafür gibt es zwei Wege.

### Einen eigenen JupyterHub einrichten

Sie können einen JupyterHub selbst aufbauen. Dafür brauchen Sie in der Regel einen Server oder eine virtuelle Maschine mit Administratorrechten, eine Adresse, unter der die Nutzer:innen den Server erreichen, eine verschlüsselte Verbindung (HTTPS) und eine Möglichkeit, Benutzerkonten zu verwalten.

Für kleinere Gruppen auf einem einzelnen Server eignet sich <a href="https://tljh.jupyter.org/" class="external-link" target="_blank">The Littlest JupyterHub</a>. Für größere Gruppen gibt es <a href="https://z2jh.jupyter.org/" class="external-link" target="_blank">Zero to JupyterHub with Kubernetes</a>. Beide Anleitungen führen Schritt für Schritt durch die Einrichtung. Einen allgemeinen Überblick bietet die <a href="https://jupyterhub.readthedocs.io/" class="external-link" target="_blank">JupyterHub Dokumentation</a>.

### Den JupyterHub Ihrer Organisation nutzen

Viele Hochschulen und Forschungseinrichtungen betreiben bereits einen JupyterHub. Dann müssen Sie keinen eigenen Server einrichten, sondern tragen die Adresse des Hubs in Ihre `_config.yml` ein. Klären Sie vorher mit Ihrem IT- oder Rechenzentrum folgende Punkte:

- **Adresse (URL):** Sie tragen sie als `jupyterhub_url` in die `_config.yml` ein.
- **Zugang:** Nur berechtigte Personen können den Hub nutzen. Fragen Sie, wer sich anmelden darf und ob ein VPN oder das Hochschulnetz nötig ist.
- **Python-Pakete:** Der Hub nutzt Ihre `requirements.txt` nicht automatisch. Geben Sie der Administration die Liste der Pakete, die Ihre Notebooks brauchen. Fragen Sie auch, ob Leser:innen fehlende Pakete selbst im Notebook installieren dürfen (zum Beispiel mit `%pip install`) und ob diese erhalten bleiben.
- **Arbeitsspeicher und Speicherplatz:** Sehr rechenintensive Notebooks können beendet werden, wenn sie mehr Speicher brauchen als erlaubt. Prüfen Sie, ob Ihre Notebooks in die Grenzen pro Person passen.
- **Aufbewahrung von Dateien:** Fragen Sie, ob gespeicherte Dateien erhalten bleiben. Wenn nicht, sollten Ihre Leser:innen ihre Ergebnisse selbst herunterladen.

```{admonition} Wichtig zu wissen
:class: keypoint

Damit der Launch-Button funktioniert, müssen auf dem JupyterHub zwei Erweiterungen installiert sein. Das erledigt in der Regel die IT-Administration, egal ob es sich um Ihren eigenen oder den Hub Ihrer Organisation handelt.

- `nbgitpuller`: Diese Erweiterung kopiert die Dateien Ihres Buches aus dem Git-Repository in die Umgebung der Nutzer:innen. Ohne sie lässt sich das Notebook über den Launch-Link nicht öffnen.

- `jupytext` (Version 0.16 oder neuer): Diese Erweiterung brauchen Sie nur, wenn Ihre Notebooks als ausführbare Markdown-Dateien (MyST Markdown) vorliegen. Sie sorgt dafür, dass der Server diese Dateien als Notebooks öffnet.
```

## Häufige Herausforderungen

**Zugang und Anmeldung**: Nur Personen mit einem Konto auf dem Hub können Notebooks starten. Prüfen Sie vorab, wer Zugang erhält und ob ein VPN oder das Hochschulnetz nötig ist.

**Notebook lässt sich nicht öffnen**: Erscheint nach dem Klick auf den Button eine Fehlerseite, ist oft `nbgitpuller` nicht installiert. Öffnet sich eine MyST-Markdown-Datei als reiner Text, fehlt meist `jupytext`. Prüfen Sie außerdem Branch und `path_to_book` in der `_config.yml`.

**Fehlende Pakete**: Der Hub nutzt nicht automatisch Ihre `requirements.txt`. Fehlt ein Paket, können Sie es in vielen Fällen direkt im Notebook installieren, zum Beispiel mit `%pip install paketname`. Ob das Paket nach dem Ende der Sitzung noch vorhanden ist, hängt vom Hub ab. Fragen Sie bei der IT-Administration nach, ob Sie Pakete selbst installieren dürfen. Besser ist es, ihr die Liste der benötigten Pakete zu geben, damit sie von Anfang an vorhanden sind.

**Begrenzte Ressourcen**: Alle Nutzer:innen teilen sich die Hardware des Servers. Wenn ein Notebook sehr viel Arbeitsspeicher braucht, kann die Sitzung beendet werden. Planen Sie bei Workshops mit vielen Teilnehmenden Zeit für anspruchsvolle Berechnungen ein.

**Speichern**: Sie arbeiten mit einer persönlichen Kopie der Dateien. Änderungen werden nicht automatisch an GitHub übertragen. Ob Ihre Dateien nach der Sitzung erhalten bleiben, hängt von der Konfiguration des Hubs ab.


## Vergleich: Colab, Binder und JupyterHub

| Merkmal | Google Colab | Binder | JupyterHub |
|---------|-------------|---------|------------|
| **Betreiber** | Google | Öffentlicher Dienst (mybinder) oder eigener BinderHub | Ihre Organisation oder Sie selbst |
| **Umgebungskontrolle** | Googles vorinstallierte Pakete; zusätzliche Pakete manuell installieren | Baut Ihre Umgebung aus Konfigurationsdateien nach | Festgelegt von der Administration; Pakete werden auf dem Server installiert |
| **Dateizugriff** | Öffnet einzelne Notebooks; Dateien manuell hochladen | Zugriff auf die gesamte Repository-Struktur | Dateien des Buches werden automatisch in Ihre Umgebung kopiert |
| **Persistenz** | Speichern in Google Drive möglich | Temporäre Sitzungen; Arbeit manuell herunterladen | Je nach Konfiguration; dauerhafter Speicherplatz möglich |
| **Datenschutz** | Notebooks liegen in Google Drive; der Code läuft auf Google-Servern und ist an Ihr Google-Konto gebunden | Öffentlicher Dienst: nicht für personenbezogene oder vertrauliche Daten geeignet; private Dateien sind nicht zugänglich | Die Organisation bestimmt, wo die Daten liegen und wer darauf zugreifen darf |
| **Setup-Aufwand** | Minimal; funktioniert sofort | Konfigurationsdateien im Repository nötig | Hub muss bereitgestellt und eingerichtet werden |
| **Anmeldung** | Google-Account | Kein Account nötig | Konto auf dem Hub nötig |
| **Ressourcen** | Mehr Rechenleistung, GPU-Zugriff möglich | Begrenzt | Abhängig von der Hardware des Servers |

JupyterHub eignet sich besonders, wenn eine Organisation Workshops oder Kurse anbietet und die Umgebung selbst kontrollieren möchte, zum Beispiel aus Gründen des Datenschutzes oder wegen größerer Rechenressourcen.


```{admonition} Zusätzliche Materialien
:class: seealso
Für detaillierte Informationen zur Konfiguration von Launch-Buttons empfehlen wir die offizielle <a href="https://jupyterbook.org/v1/interactive/launchbuttons.html" class="external-link" target="_blank">Jupyter Book Dokumentation zu Launch Buttons</a>.

Eine Einführung in JupyterHub finden Sie in der <a href="https://jupyterhub.readthedocs.io/" class="external-link" target="_blank">offiziellen JupyterHub Dokumentation</a>. Für einen einfachen Hub auf einem einzelnen Server empfehlen wir <a href="https://tljh.jupyter.org/" class="external-link" target="_blank">The Littlest JupyterHub</a>. Für größere Installationen mit Kubernetes gibt es <a href="https://z2jh.jupyter.org/" class="external-link" target="_blank">Zero to JupyterHub with Kubernetes</a>.

Informationen zu den Erweiterungen, die der Server benötigt, finden Sie in der <a href="https://nbgitpuller.readthedocs.io/" class="external-link" target="_blank">nbgitpuller Dokumentation</a> und in der <a href="https://jupytext.readthedocs.io/en/latest/formats-markdown.html#myst-markdown" class="external-link" target="_blank">Jupytext Dokumentation zu MyST Markdown</a>.
```
