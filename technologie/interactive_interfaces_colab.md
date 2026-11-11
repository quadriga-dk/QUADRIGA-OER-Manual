# Interaktive Rechenumgebungen mit Google Colab

Da Jupyter Books auf Jupyter-Notebooks oder ausführbaren Markdown-Dateien basieren, ist es möglich, über einen Launch-Button direkt in der Cloud interaktive Jupyter-Sessions zu starten. So können Leser:innen Inhalte in einer vertrauten Coding-Umgebung live ausprobieren, ohne etwas zu installieren. Im <a href="https://github.com/quadriga-dk/Book_Template" class="external-link" target="_blank"><code>Book_Template</code></a> ist Google Colab – eine kostenlose Cloud-Lösung für Jupyter Notebooks – bereits vorkonfiguriert. Diese Seite erklärt, wie Sie die Funktion für Ihre eigene OER aktivieren und was Sie dabei beachten sollten.


## Technische Konfiguration
Damit die Launch-Buttons in Ihrem Jupyter Book erscheinen, muss die Datei `_config.yml` entsprechend konfiguriert werden. Im `Book_Template` ist diese Konfiguration bereits enthalten; die folgenden Zeilen zeigen, welche Einträge dafür verantwortlich sind. Fügen Sie sie in Ihre `_config.yml` ein, wenn sie dort noch fehlen:

```yaml
launch_buttons:
    # Konfiguration für Google Colab
    colab_url: https://colab.research.google.com
```

Diese Konfiguration aktiviert die Google Colab Launch-Buttons für alle kompatiblen Notebooks in Ihrem Buch. Ob ein Kapitel einen Button erhält, hängt davon ab, ob es als ausführbares Notebook bzw. als ausführbare Markdown-Datei vorliegt.

## Was Sie beim Aktivieren beachten sollten

Der Launch-Button öffnet ausschließlich das ausgewählte Notebook in Google Colab – nicht den gesamten Projektordner. Für die Konzeption Ihrer OER bedeutet das:

- **Dateien mitliefern:** Legen Sie alle Dateien, die ein Notebook benötigt (Daten, Bilder, Hilfsskripte), so ab, dass das Notebook sie selbst laden kann – zum Beispiel über einen Download aus dem öffentlichen GitHub-Repositorium oder über eine Setup-Zelle, die die Dateien beschafft.
- **Setup-Zellen vorsehen:** Fassen Sie Installationen und das Laden von Daten in Zellen am Anfang des Notebooks zusammen. Leser:innen können das Notebook dann von oben nach unten ausführen, ohne manuell nachzuarbeiten.
- **Pakete berücksichtigen:** Colab bringt viele Pakete bereits mit, aber nicht alle, die Ihre OER benötigt. Nennen Sie fehlende Pakete in einer Setup-Zelle (etwa `%pip install paketname`) und weisen Sie im Kapitel darauf hin.
- **Funktion testen:** Prüfen Sie den Button in der gebauten Version Ihres Buches und führen Sie das Notebook einmal vollständig in Colab aus. So erkennen Sie fehlende Pakete oder Dateizugriffe, bevor Ihre Lernenden darauf stoßen.
- **Geeignete Inhalte wählen:** Colab eignet sich für Notebooks, die ohne lokale Daten und ohne vertrauliche Daten auskommen. Für reproduzierbare Umgebungen mit exakt festgelegten Paketversionen ist Binder oder ein JupyterHub die bessere Wahl.

## Nutzung durch Lernende

Wie Lernende ein Notebook in der Cloud öffnen und ausführen, fehlende Pakete nachinstallieren, auf Dateien zugreifen und ihre Ergebnisse speichern, ist ausführlich im Learners Manual beschrieben: <a href="https://quadriga-dk.github.io/QUADRIGA-Learners-Manual/nutzung/modi/cloud.html" class="external-link" target="_blank">Cloud-Ausführung im Learners Manual</a>. Verweisen Sie in Ihrer OER auf diese Seite, statt die Hinweise im Buch selbst zu wiederholen.

## Alternative Plattformen

Neben Google Colab existieren weitere Plattformen für interaktive Notebooks:

- **Binder**: Ermöglicht die Ausführung von Notebooks ohne Installation und kann ganze Projektordner öffnen

- **JupyterHub**: Wird häufig von Universitäten und Organisationen für gehostete Notebooks eingesetzt

Google Colab bietet für die meisten Lernenden den einfachsten Einstieg und wird daher in dieser Anleitung als primäre Plattform behandelt. Die Konfiguration der anderen Plattformen ist auf den jeweiligen Unterseiten beschrieben.


```{admonition} Zusätzliche Materialien
:class: seealso
Für detaillierte Informationen zur Konfiguration von Launch-Buttons in Jupyter Book empfehlen wir die offizielle <a href="https://jupyterbook.org/en/stable/interactive/launchbuttons.html" class="external-link" target="_blank">Jupyter Book Dokumentation zu Launch Buttons</a>. Diese enthält wichtige technische Details zur Integration verschiedener interaktiver Plattformen in Ihr eigenes Jupyter Book.
```
