(formatierung:video_abbildungen)=

# Videos als Abbildungen

Kurze Animationen – etwa eine Abfolge von Screenshots oder eine bewegte Grafik – werden häufig als animiertes GIF eingebunden. Eine MP4-Datei ist bei gleicher Qualität jedoch ca. 20-mal kleiner, weshalb diese bevorzugt sind. QUADRIGA-Bücher stellen deshalb `{figure}`-Umgebungen, deren Ziel eine Videodatei ist, als HTML5-Video dar.

## Verwendung

Eine Videodatei wird wie eine Abbildung eingebunden. Alles, was Sie von `{figure}` kennen, funktioniert unverändert: `align`, `width`, `name` für Verweise und `alt` als Textbeschreibung für Screenreader. Unterstützt werden `.mp4`, `.webm` und `.ogv`.

````
```{figure} ../assets/formatierung/video_demo.mp4
---
align: left
width: 100%
name: beispiel-video-abbildung
alt: Beispielvideo: Ein weißer Punkt wandert über einen blauen Hintergrund.
---
Beispiel einer animierten Abbildung.
```
````

```{figure} ../assets/formatierung/video_demo.mp4
---
align: left
width: 100%
name: beispiel-video-abbildung
alt: Beispielvideo: Ein weißer Punkt wandert über einen blauen Hintergrund.
---
Beispiel einer animierten Abbildung.
```

Die Dateien werden beim Build nach `_videos/` kopiert und in der Bildunterschrift durch ein kleines Play-Symbol gekennzeichnet.

## Verhalten

Die Videos starten stumm und in einer Schleife. Eingeblendete Bedienelemente gibt es nicht – ein Klick auf das Video hält die Animation an und startet sie wieder (ebenso `Leertaste` oder `Enter`, wenn das Video den Fokus hat). Scrollt ein Video aus dem sichtbaren Bereich, pausiert es, damit eine Seite mit mehreren Animationen nicht unnötig Rechenzeit verbraucht.

```{admonition} Hinweis
:class: hinweis
Wer die Animation nicht sehen kann, ist auf den `alt`-Text angewiesen. Beschreiben Sie dort, was die Animation zeigt – nicht nur, dass es eine Animation ist.
```

## Einrichtung im Buch

Die Funktion besteht aus `_ext/video_figure.py` (Rendering), `_static/video-figure.js` (Play/Pause) und den zugehörigen Regeln in `_static/quadriga.css`. Die Dateien sind im <a
    href="https://github.com/quadriga-dk/Book_Template"
    class="external-link" target="_blank"><code>Book_Template</code></a>
enthalten; in `_config.yml` müssen Erweiterung und Skript registriert sein:

```yaml
sphinx:
    local_extensions:
        video_figure: _ext
    config:
        html_js_files:
            - carousel.js
            - video-figure.js
```

## Von GIF zu MP4

Ein vorhandenes GIF lässt sich mit `ffmpeg` umwandeln:

```bash
ffmpeg -i eingabe.gif -an -c:v libx264 -preset slow -crf 23 \
  -pix_fmt yuv420p -movflags +faststart ausgabe.mp4
```

Das Ergebnis hat dieselbe Abspielzeit und Bildrate wie die Vorlage, benötigt aber nur einen Bruchteil des Speicherplatzes. Prüfen Sie danach im gebauten Buch, ob die Animation flüssig läuft und der `alt`-Text den Inhalt beschreibt.
