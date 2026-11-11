(Checkliste_neue_OER)=
# Checkliste neue OER
Die nachfolgende Checkliste hilft Ihnen, wenn Sie eine neue OER mit dem <a
    href="https://github.com/quadriga-dk/Book_Template"
    class="external-link" target="_blank"><code>Book_Template</code></a>
erstellen. Sie bietet einen Überblick über alle Schritte von der Planung bis zur
Veröffentlichung. Verweise auf Kapitel und Abschnitte beziehen sich jeweils auf
diese Anleitung, in der die einzelnen Punkte erläutert werden.

Eine Demo-Version der Vorlage finden Sie unter <a
    href="https://quadriga-dk.github.io/Book_Template/"
    class="external-link" target="_blank">https://quadriga-dk.github.io/Book_Template/</a>.


## Repositorium anlegen
- [ ] <a href="https://github.com/quadriga-dk/Book_Template"
    class="external-link" target="_blank"><code>Book_Template</code></a>
    als neues Repositorium angelegt
  - in GitHub über die Funktion "Use this template"
  - oder per Download der Vorlage als `.zip`-Datei und Ablegen der Inhalte in einem neuen Repositorium

## Planung und Strukturierung
- [ ] Fallstudie identifiziert mit konkreter Forschungsfrage und authentischen Daten
- [ ] Zielgruppe und erforderliches Vorwissen klar definiert
- [ ] Struktur nach Datenzyklus/Forschungsprozess ausgerichtet
- [ ] 3 Groblernziele (Kapitel) definiert (+Einstieg, Fragestellung, Reflexion/Resümee, und Abschluss)
- [ ] Feinlernziele nach ABCD-Prinzip formuliert (Audience, Behavior, Condition, Degree)
- [ ] Bloom'sche Taxonomie für kognitive Lernzielformulierung verwendet
- [ ] Geschätzter Workload pro Kapitel (1-3 Stunden) festgelegt
- [ ] Geschätzter Workload pro Abschnitt (20-60 Minuten) festgelegt

## Didaktische Komponenten
- [ ] Zugangswege definiert (Book-Only, Cloud, Local)
- [ ] Interaktive Übungen (pro Modul 1-4) pro Kapitel eingebaut
- [ ] Assessment-Elemente am Ende jedes Kapitels integriert


## Inhaltliche Qualitätssicherung
- [ ] Fachliche Korrektheit überprüft
- [ ] Code-Beispiele kommentiert und verständlich
- [ ] Alle Fachbegriffe erklärt oder verlinkt
- [ ] ggf. interdisziplinäre Anwendbarkeit berücksichtigt
- [ ] ggf. Transfermöglichkeiten zu anderen Kontexten aufgezeigt

## Strukturelle Qualitätssicherung
- [ ] Einheitliche Formatierung und Layout
- [ ] Visuelle Elemente (Diagramme, Grafiken) eingesetzt
- [ ] Quellennachweise und Literaturverweise vollständig
- [ ] Bilder mit Alt-Texten für Barrierefreiheit versehen

## Git Repositorium
- [ ] Inhalte des `Book_Template` vollständig in das neue Git-Repositorium übernommen
  - entweder "von Hand" per Download und Kopieren der relevanten Dateien
  - in GitHub, per Template-Funktionalität
- [ ] Sichtbarkeit und Zugriffsrechte korrekt konfiguriert

### ggf. GitHub Actions und GitHub Pages
- [ ] GitHub Pages korrekt konfiguriert
- [ ] passende GitHub Action(s) ausgewählt
  - [ ] Action angepasst
  - [ ] unnötige Actions gelöscht oder deaktiviert

## `_config.yml`
- [ ] Metadaten in der Konfigurationsdatei angepasst
- [ ] GitHub/GitLab/…-Verknüpfungen konfiguriert
- [ ] Integrationen (Issues, Binder, Colab, …) konfiguriert
- [ ]

## `_toc.yml`
- [ ] Anpassen des ToC auf minimales Beispiel
- [ ] Struktur des Repositoriums (Ordner und Unterordner) definiert

## ggf. Design
- [ ] Anpassung von Logos
- [ ] Anpassung von Farben

## Aufräumen
- [ ] Entfernen nicht benötigter Inhalte aus Ihrer Kopie des `Book_Template`

## `README.md`
- [ ] `README.md` angepasst

## Technische Überprüfung
- [ ] Alle Abhängigkeiten und Datensätze dokumentiert
- [ ] Dateipfade relativ und plattformunabhängig gestaltet
- [ ] Build-Prozess erfolgreich ohne Fehler (jb build .)
- [ ] Responsive Design getestet (verschiedene Bildschirmgrößen)
- [ ] Links (intern und extern) funktionieren
- [ ] Downloadbare Ressourcen funktionieren
- [ ] Assessment-Feedback-Mechanismen getestet

## Fertigstellung und Veröffentlichung
