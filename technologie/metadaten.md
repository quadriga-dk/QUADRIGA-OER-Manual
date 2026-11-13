(technologie:metadaten)=

# Metadaten

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

Metadaten beschreiben eine OER so, dass sie von Menschen und Maschinen
gefunden, eingeordnet und nachgenutzt werden kann. In diesem Kapitel lernen Sie
zuerst das _QUADRIGA Application Profile_ für OERs kennen. Anschließend wird
gezeigt, wie dieses in der Datei `quadriga-metadata.yml` konkret umgesetzt wird.
Zum Abschluss werden die tatsächlichen Metadaten dieser Anleitung sowie die
daraus automatisch erzeugten Exportformate erläutert.

````{admonition} Hinweis zur Version 2.0.0
:class: hinweis

Dieses Kapitel beschreibt das QUADRIGA Application Profile in der **Version
2.0.0**. Gegenüber der Version 1.0.0 haben sich sowohl die Feldnamen (nun
`camelCase` statt `kebab-case`) als auch der Dateiname der Metadatendatei
(`quadriga-metadata.yml` statt `metadata.yml`) geändert. Eine Übersicht der
Änderungen und ein Konvertierungsskript finden Sie im Abschnitt
{ref}`technologie:metadaten:migration`.
````

## Entitäten und Konventionen

Das QUADRIGA Application Profile ist als <a href="https://json-schema.org"
    target="_blank" class="external-link">JSON-Schema</a> (Draft 2020-12)
implementiert und modular aufgebaut: `schema.json` beschreibt die OER als
oberste Entität, weitere Dateien wie `Chapter.json`, `LearningObjective.json`,
`Author.json` oder `MultilingualText.json` beschreiben die referenzierten
Entitäten und Datentypen. Insgesamt besteht das Schema aus wenigen, klar
abgegrenzten Entitäten:

| Entität                     | Datei                     | Beschreibung                         |
| --------------------------- | ------------------------- | ------------------------------------ |
| `OpenEducationalResource`   | `schema.json`             | die OER als Ganzes (Top-Level)       |
| `Author` / `Contributor`    | `Author.json`, `Contributor.json` | Personen als Urheber:innen bzw. Mitwirkende |
| `Chapter`                   | `Chapter.json`            | ein Kapitel der OER                  |
| `LearningObjective`         | `LearningObjective.json`  | ein Lernziel eines Kapitels          |
| `SupplementalMaterial`      | `SupplementalMaterial.json` | nachgenutztes Material             |
| `UsedTool`                  | `UsedTool.json`           | ein in der OER verwendetes Werkzeug  |

Hinzu kommen gemeinsam genutzte Datentypen wie `MultilingualText.json` (Text in
einer oder mehreren Sprachen), `SemVer.json`, `timeRequired.json`,
`language.json`, `license.json`, `credit.json` und `orcid.json`.

Für die Feldnamen gelten zwei Konventionen:

- **`camelCase`:** Feldnamen werden ohne Trennzeichen und mit großgeschriebenen
  Wortanfängen notiert, bspw. `timeRequired` oder `dateModified`.
- **Suffix `LIST`:** Eigenschaften, die eine Liste von Objekten enthalten,
  enden auf `LIST` – bspw. `authorLIST`, `chapterLIST` oder
  `learningObjectiveLIST`. Das macht im YAML sofort sichtbar, ob ein einzelnes
  Objekt oder eine Liste erwartet wird.

## Die Datei `quadriga-metadata.yml`

Für die Definition der Metadaten im Jupyter Book wurde <a href="https://yaml.org"
    target="_blank" class="external-link">YAML</a> gewählt, da es durch
OER-Autor:innen einfach geschrieben und gleichzeitig gut automatisch verarbeitet
werden kann.

Die Metadaten werden in der Datei `quadriga-metadata.yml` im Wurzelverzeichnis
des Jupyter Books gespeichert. Diese Datei ist die _einzige Quelle_ der
Metadaten (_single source of truth_): Alle weiteren Metadatendateien im
Repositorium werden daraus automatisch erzeugt und sollten nicht manuell
bearbeitet werden (siehe Abschnitt {ref}`technologie:metadaten:export-formate`).
Insbesondere die ebenfalls im Wurzelverzeichnis liegende Datei `metadata.yml`
wird für die OERSI-Suche generiert und darf nicht von Hand gepflegt werden.

Eine Metadatenbeschreibung gilt als valide, wenn sie alle Pflichtfelder enthält
und technisch korrekt umgesetzt ist. Um Fehler früh zu erkennen, empfiehlt es
sich, die Schemaversion in der ersten Zeile der Datei als Kommentar für den
_yaml-language-server_ zu hinterlegen. Viele Editoren (z. B. VS Code oder
Neovim) bieten dann Autovervollständigung und eine Prüfung direkt beim
Schreiben:

```yaml
# yaml-language-server: $schema=https://quadriga-dk.github.io/quadriga-schema/v2.0.0/schema.json
```

### Empfohlene Reihenfolge der Felder

Die Reihenfolge der Felder ist technisch nicht relevant, erleichtert aber die
Lesbarkeit und den Vergleich zwischen OERs. Empfohlen wird diese kanonische
Reihenfolge (Pflichtfelder mit ⭐):

```
- title⭐
- authorLIST⭐
- keywordLIST⭐
- description⭐
- tableOfContents⭐
- disciplineLIST⭐
- researchObjectTypeLIST⭐
- targetGroupLIST⭐
- timeRequired⭐
- language⭐
- contributorLIST
- identifier⭐
- identifierGit⭐
- identifierOER⭐
- prerequisiteLIST
- usedToolLIST
- chapterLIST⭐
  - title⭐
  - description⭐
  - url⭐
  - timeRequired⭐
  - learningGoal⭐
  - learningObjectiveLIST⭐
    - description⭐
    - competency⭐
    - dataFlow⭐
    - bloomsCategory⭐
    - assessment
  - supplementalMaterialLIST
    - title⭐
    - url
  - language
- dateIssued⭐
- dateModified⭐
- version⭐
- contextOfCreation⭐
- qualityAssurance⭐
- learningResourceType⭐
- schemaVersion⭐
- license⭐
- licenseCode
```

Ein vollständiges, wenn auch verkürztes Beispiel finden Sie als <a
    href="https://github.com/quadriga-dk/quadriga-schema/blob/main/examples/quadriga-metadata.yml"
    target="_blank" class="external-link">`examples/quadriga-metadata.yml`</a>
im Repositorium des Application Profiles. Dort liegt zusätzlich eine <a
    href="https://github.com/quadriga-dk/quadriga-schema/blob/main/examples/quadriga-metadata.xml"
    target="_blank" class="external-link">XML-Variante desselben
Beispiels</a>.

## Felder

Im Folgenden werden die Felder des QUADRIGA Application Profiles beschrieben.
Pflichtfelder sind mit ⭐ gekennzeichnet. Wo ein kontrolliertes Vokabular
vorgegeben ist, sind die erlaubten Werte aufgeführt; die vollständige und
jederzeit aktuelle Liste finden Sie in der <a
    href="https://quadriga-dk.github.io/quadriga-schema/" target="_blank"
    class="external-link">HTML-Dokumentation des Schemas</a>.

### Angaben zur OER

(metadata:title)=

#### `title`⭐

Titel der OER. Ein etwaiger Untertitel wird mit `": "` vom Titel getrennt im
selben Feld angegeben; ein eigenes Untertitel-Feld gibt es nicht.

(metadata:authors)=

#### `authorLIST`⭐

Liste der Autor:innen der OER im Sinne des Urheberrechts. Es muss mindestens
eine Person angegeben werden. Der Aufbau der Personenobjekte ist unter
{ref}`Personen <metadata:person>` beschrieben.

(metadata:keywords)=

#### `keywordLIST`⭐

Liste von Schlag-/Stichwörtern, welche die OER und ihre Inhalte beschreiben. Es
muss mindestens ein Stichwort angegeben werden. Jedes Stichwort ist ein
mehrsprachiger Text (siehe
{ref}`mehrsprachige Texte <metadata:multilingual-text>`), sodass bspw.
deutsche und englische Schlagwörter parallel erfasst werden können:

```yaml
keywordLIST:
  - Open Educational Resources
  - de: Datenkompetenz
    en: Data Literacy
```

(metadata:description)=

#### `description`⭐

Beschreibung der OER als Freitext (mehrsprachig möglich). Die Beschreibung
sollte Umfang, Zielsetzung und Besonderheiten der OER zusammenfassen.

(metadata:table-of-contents)=

#### `tableOfContents`⭐

Inhaltsverzeichnis der OER als Freitext, typischerweise als Markdown-Liste der
Kapitelüberschriften.

(metadata:discipline)=

#### `disciplineLIST`⭐

Disziplinen, die bei der Erstellung der OER im Fokus standen. Es können eine bis
drei Werte aus diesem kontrollierten Vokabular ausgewählt werden:

- `Verwaltungswissenschaften`
- `Digital Humanities`
- `Informatik`
- `Informationswissenschaft`
- `übergreifend`

(metadata:research-object-type)=

#### `researchObjectTypeLIST`⭐

Datentyp, der vorrangig in der OER behandelt wird. Es können einer bis zwei
Werte aus diesem kontrollierten Vokabular ausgewählt werden:

- `Text`
- `Tabelle`
- `Bewegtes Bild`
- `übergreifend`

(metadata:target-group)=

#### `targetGroupLIST`⭐

Zielgruppe der OER. Es können eine bis vier Werte aus diesem kontrollierten
Vokabular ausgewählt werden:

- `Forschende (PostDoc)`
- `Forschende (Projektleitung)`
- `Promovierende`
- `Hochschullehrende`

(metadata:time-required)=

#### `timeRequired`⭐

Angedachte Bearbeitungsdauer für Lernende im ISO-8601-Duration-Format (siehe <a
    href="https://en.wikipedia.org/wiki/ISO_8601#Durations" target="_blank"
    class="external-link">Wikipedia-Artikel zu ISO 8601</a>). Beispiele:

- `PT16H15M` für 16 Stunden und 15 Minuten
- `P1DT10S` für 1 Tag und 10 Sekunden

Typischerweise werden Angaben zur Bearbeitungsdauer in Stunden und Minuten
gemacht.

(metadata:language)=

#### `language`⭐

Sprache der OER als ISO-639-1-Sprachcode aus zwei Kleinbuchstaben – bspw. `de`
oder `en`.

(metadata:contributors)=

#### `contributorLIST`

Liste der Mitarbeiter:innen bzw. Beitragenden, die nicht Autor:innen im Sinne
des Urheberrechts sind (z. B. Softwareentwicklung, redaktionelle Unterstützung).
Das Feld ist optional; der Aufbau der Personenobjekte entspricht dem von
{ref}`authorLIST <metadata:authors>` und ist unter
{ref}`Personen <metadata:person>` beschrieben.

(metadata:identifier)=

#### `identifier`⭐

Eindeutiger persistenter Identifier der OER in Form einer DOI (als URI). Die DOI
identifiziert das gesamte Buch, typischerweise die von Zenodo vergebene DOI.

(metadata:identifier-git)=

#### `identifierGit`⭐

URL des Git-Repositoriums, in dem die OER-Inhalte liegen.

(metadata:identifier-oer)=

#### `identifierOER`⭐

URL der Startseite der OER in der Leseansicht (Website).

(metadata:prerequisites)=

#### `prerequisiteLIST`

Liste von Voraussetzungen bzw. Vorkenntnissen, welche Lernende für die
erfolgreiche Bearbeitung der OER mitbringen sollten. Jeder Eintrag ist ein
mehrsprachiger Text.

(metadata:used-tools)=

#### `usedToolLIST`

Liste von Werkzeugen bzw. (Software-)Tools, die bei der Bearbeitung der OER
verwendet werden. Jeder Eintrag ist ein Objekt aus `name`⭐ (mehrsprachiger
Text) und `url`; als URL wird ein möglichst persistenter Link empfohlen, bspw.
aus der <a href="https://id.loc.gov/authorities/subjects.html" target="_blank"
    class="external-link">Library of Congress Subject Headings</a>:

```yaml
usedToolLIST:
  - name: R (Programmiersprache)
    url: http://id.loc.gov/authorities/subjects/sh2002004407
  - name: RStudio
    url: https://posit.co/download/rstudio-desktop/
```

(metadata:chapters)=

#### `chapterLIST`⭐

Liste der Kapitel der OER. Es muss mindestens ein Kapitel angegeben werden. Der
Aufbau der Kapitelobjekte ist im Abschnitt {ref}`Kapitel <metadata:chapter>`
beschrieben.

(metadata:date-issued)=

#### `dateIssued`⭐

Datum der Erstveröffentlichung der OER im Format `YYYY-MM-DD`.

(metadata:date-modified)=

#### `dateModified`⭐

Datum der letzten (großen, inhaltlich umfangreichen) Änderung im Format
`YYYY-MM-DD`. Sollte immer mit einer Versionsänderung
({ref}`version <metadata:version>`) einhergehen. Verbesserungen von Grammatik und
Orthographie verlangen nicht zwingend die Erstellung einer neuen Version. Dieses
Datum muss jedoch aktualisiert werden, wenn eine neue Version auf Zenodo
veröffentlicht wird (bspw. über die Release-Funktion auf GitHub). In der
GitHub Action `update-metadata.yml` wird das Feld beim Setzen eines
Versions-Tags automatisch aktualisiert.

(metadata:version)=

#### `version`⭐

Version der OER im <a href="https://semver.org" target="_blank"
    class="external-link">SemVer</a>-Format (`MAJOR.MINOR.PATCH`). Eine
Versionsänderung korrespondiert auch immer mit einer Änderung von
{ref}`dateModified <metadata:date-modified>`.

(metadata:context-of-creation)=

#### `contextOfCreation`⭐

Beschreibung des Entstehungskontextes der OER, bspw. Hinweise auf Förderung
oder beteiligte Communities. Für QUADRIGA-OERs ist ein Standardwert vorgegeben:

```yaml
contextOfCreation: 'Die vorliegenden Open Educational Resources wurden durch das
  Datenkompetenzzentrum QUADRIGA erstellt.

  Förderkennzeichen: 16DKZ2034A-H'
```

(metadata:quality-assurance)=

#### `qualityAssurance`⭐

Nachweis der Qualitätssicherung als Objekt mit zwei Pflichtfeldern:

- `description`: Link zu einem veröffentlichten Qualitätssicherungskonzept
  (bevorzugt als DOI, also beginnend mit `https://doi.org/`) oder eine
  textliche Beschreibung der durchgeführten Maßnahmen.
- `date`: Datum der abgeschlossenen Qualitätsprüfung im Format `YYYY-MM-DD`.

```yaml
qualityAssurance:
  description: https://doi.org/10.5281/zenodo.18953896
  date: '2026-11-14'
```

(metadata:type-of-learning-resource)=

#### `learningResourceType`⭐

(Material-)Format der OER als mehrsprachiger Text. In QUADRIGA ist dies
typischerweise `Jupyter Book`.

(metadata:schema-version)=

#### `schemaVersion`⭐

Versionsnummer des Application Profiles, das den vorliegenden Metadaten
zugrunde liegt. Das kontrollierte Vokabular enthält aktuell genau einen Wert:
`2.0.0`. Wird das Application Profile verändert oder erweitert, so wird eine
neue Version definiert. Vorherige, veröffentlichte Versionen bleiben bestehen,
können jedoch als _deprecated_ markiert werden.

(metadata:license)=

#### `license`⭐

URL der freien Lizenz für die Inhalte der OER. Empfohlen wird eine
CC-Lizenz, bspw. `https://creativecommons.org/licenses/by-sa/4.0/`.

(metadata:license-code)=

#### `licenseCode`

URL der Lizenz für den in der OER enthaltenen Programmcode, sofern zutreffend
(bspw. `https://opensource.org/licenses/MIT`). Sobald die OER Code enthält,
wird die Festlegung einer eigenen Code-Lizenz empfohlen, da CC-Lizenzen – mit
Ausnahme von CC0 – für Programmcode nicht geeignet sind.

### Kapitel

(metadata:chapter)=

Ein Eintrag in `chapterLIST` beschreibt ein Kapitel der OER.

(metadata:chapter-title)=

#### `title`⭐ (in `chapterLIST`)

Kapitelüberschrift, wie sie in diesem Kapitel verwendet wird. Kann als
einfacher Text oder als mehrsprachiger Text angegeben werden.

(metadata:chapter-description)=

#### `description`⭐ (in `chapterLIST`)

Beschreibung des Kapitelinhalts. Bietet eine Übersicht darüber, was in diesem
Kapitel behandelt wird.

(metadata:chapter-url)=

#### `url`⭐ (in `chapterLIST`)

URL zum direkten Zugriff auf die erste Seite der Leseansicht (Website) des
Kapitels.

(metadata:chapter-time-required)=

#### `timeRequired`⭐ (in `chapterLIST`)

Angedachte Bearbeitungsdauer für Lernende, spezifisch für dieses Kapitel, im
ISO-8601-Duration-Format.

(metadata:learning-goal)=

#### `learningGoal`⭐ (in `chapterLIST`)

Übergeordnetes Lernziel des Kapitels als kurze, prägnante Formulierung. Es gibt
einen groben Überblick über die im Kapitel zu erlernenden Inhalte.

(metadata:learning-objectives)=

#### `learningObjectiveLIST`⭐ (in `chapterLIST`)

Liste der Lernziele des Kapitels; mindestens ein Lernziel ist erforderlich. Der
Aufbau der Lernzielobjekte ist im Abschnitt
{ref}`Lernziele <metadata:learning-objective>` beschrieben.

(metadata:supplemented-by)=

#### `supplementalMaterialLIST` (in `chapterLIST`)

Liste nachgenutzter Materialien, die im Kapitel verwendet werden. Jeder Eintrag
enthält `title`⭐ (Titel oder Name des Materials) und `url` (bevorzugt ein
persistenter Link, z. B. eine DOI).

(metadata:chapter-language)=

#### `language` (in `chapterLIST`)

Sprache des Kapitels als ISO-639-1-Sprachcode. Nur angeben, wenn die Sprache des
Kapitels von der Sprache der OER ({ref}`language <metadata:language>`) abweicht.

### Lernziele

(metadata:learning-objective)=

Ein Eintrag in `learningObjectiveLIST` beschreibt ein einzelnes Lernziel eines
Kapitels.

(metadata:learning-objective-description)=

#### `description`⭐ (in `learningObjectiveLIST`)

Formulierung des Lernziels, bspw. strukturiert nach Schermutzki (2007).
Mehrsprachige Angabe ist möglich.

(metadata:competency)=

#### `competency`⭐ (in `learningObjectiveLIST`)

Kompetenz, die im Lernziel fokussiert wird, nach dem <a
    href="https://doi.org/10.5281/zenodo.14747822" target="_blank"
    class="external-link">QUADRIGA-Datenkompetenzframework</a>. Es muss ein Wert
aus diesem kontrollierten Vokabular gewählt werden:

- `Orientierungswissen`
- `1.1 Identifikation`, `1.2 Qualitätssicherung`, `1.3 Ethik und Recht`
- `2.1 Erhebung`, `2.2 Validierung`, `2.3 Aufbereitung`
- `3.1 Organisation`, `3.2 Erschließung`
- `4.1 Datenanalyse`, `4.2 Visualisierung`, `4.3 Interpretation`
- `5.1 Aufbewahrung`, `5.2 Datenpublikation`, `5.3 Kommunikation`
- `nicht anwendbar`

(metadata:data-flow)=

#### `dataFlow`⭐ (in `learningObjectiveLIST`)

Schritt im Datenfluss, dem die Kompetenz zugeordnet ist. Es muss ein Wert aus
diesem kontrollierten Vokabular gewählt werden:

- `übergreifend`
- `1 Planung`
- `2 Erhebung und Aufbereitung`
- `3 Management`
- `4 Analyse`
- `5 Publikation und Nachnutzung`
- `nicht anwendbar`

(metadata:blooms-category)=

#### `bloomsCategory`⭐ (in `learningObjectiveLIST`)

Kategorie der Bloomschen Lerntaxonomie, welcher das Lernziel zugeordnet ist. Aus
der Kombination der Zuordnungen der Lernziele eines Kapitels lässt sich ein
allgemeines Kompetenzniveau ("Basis", "Fortgeschritten", "Expert:in") ableiten.
Es muss ein Wert aus diesem kontrollierten Vokabular gewählt werden:

- `1 Erinnern`
- `2 Verstehen`
- `3 Anwenden`
- `4 Analysieren`
- `5 Bewerten`
- `6 Erschaffen`
- `nicht anwendbar`

(metadata:assessment)=

#### `assessment` (in `learningObjectiveLIST`)

Art der Lernstandskontrolle für dieses Lernziel als mehrsprachiger Text, bspw.
`Multiple-Choice-Quiz, Reflexionsfragen`.

### Personen

(metadata:person)=

Autor:innen und Beitragende werden in Version 2.0.0 immer als Objekt mit
folgenden Eigenschaften angegeben:

- `givenName`⭐ – Vorname
- `familyName`⭐ – Nachname. Liegt kein Nachname vor, wird das Feld mit einer
  leeren Zeichenkette belegt und der vollständige Name in `givenName`
  eingetragen.
- `orcid` – ORCID als URI im Format
  `https://orcid.org/XXXX-XXXX-XXXX-XXXX`. Die Angabe einer <a
  href="https://orcid.org" target="_blank" class="external-link">ORCID</a> wird
  dringend empfohlen.
- `affiliation` – institutionelle Zugehörigkeit, nach Möglichkeit mit
  <a href="https://ror.org" target="_blank" class="external-link">ROR</a>-ID.
- `creditLIST` – Liste der übernommenen Rollen nach der <a
  href="https://credit.niso.org" target="_blank"
  class="external-link">CRediT-Taxonomie</a>. Erlaubt sind:
  `Conceptualization`, `Data curation`, `Formal analysis`,
  `Funding acquisition`, `Investigation`, `Methodology`,
  `Project administration`, `Software`, `Resources`, `Supervision`,
  `Validation`, `Visualization`, `Writing – original draft`,
  `Writing – review & editing`.

Ein Personeneintrag sieht damit bspw. so aus:

```yaml
authorLIST:
  - familyName: Schnaitter
    givenName: Hannes
    orcid: https://orcid.org/0000-0002-1602-6032
    affiliation: Humboldt-Universität zu Berlin (https://ror.org/01hcx6992)
    creditLIST:
      - Writing – original draft
      - Software
```

### Gemeinsam genutzte Datentypen

(metadata:multilingual-text)=

#### `MultilingualText`

Natürlichsprachliche Texte werden standardmäßig auf Deutsch verfasst und können
als einfache Zeichenkette notiert werden. Soll die Sprache explizit gemacht
werden und/oder sollen mehrere Sprachen angegeben werden, so wird statt der
Zeichenkette ein Objekt mit ISO-639-1-Sprachcodes als Schlüssel verwendet:

```yaml
description:
  de: Beschreibung der OER auf Deutsch.
  en: Description of the OER in English.
```

Es muss mindestens eine Sprache angegeben werden.

(metadata:semver)=

#### `SemVer`

Ein Bezeichner nach dem <a href="https://semver.org" target="_blank"
    class="external-link">Semantic Versioning 2.0.0</a>-Format. Wird bei der
Versionierung des Schemas und der OER verwendet. Besteht aus Major-, Minor- und
Patch-Version (z. B. `1.1.0`), optional gefolgt von
Pre-Release-Identifikatoren und Build-Metadaten.

## `quadriga-metadata.yml` dieser Anleitung

```{literalinclude} /quadriga-metadata.yml
:language: yaml
:linenos:
```

(technologie:metadaten:json-schema)=

## JSON-Schema und Validierung

Das JSON-Schema ist im Repositorium <a
    href="https://github.com/quadriga-dk/quadriga-schema" target="_blank"
    class="external-link">quadriga-schema</a> definiert. Auf Basis dieses
Repositoriums wird eine <a href="https://quadriga-dk.github.io/quadriga-schema/schema.html"
    target="_blank" class="external-link">interaktive Darstellung</a> sowie der
<a href="https://quadriga-dk.github.io/quadriga-schema/latest/schema.json"
    target="_blank" class="external-link">Einstieg für die Nutzung in anderen
Schemas oder in Verifikationstools (`schema.json` hier im Versionsalias
`latest`)</a> generiert. Für die Verwendung in Werkzeugen sollte immer eine
bestimmte Version festgelegt werden – bspw.
<https://quadriga-dk.github.io/quadriga-schema/v2.0.0/schema.json>. Die
referenzierten Teil-Schemas (etwa `Chapter.json`) werden relativ zur
`schema.json` aufgelöst.

Die Validierung erfolgt in QUADRIGA-OERs automatisch im Build-Prozess: Das
Skript `quadriga/metadata/validate_schema.py` lädt das Schema (und die
referenzierten Teil-Schemas), cached sie lokal im Verzeichnis `.schema_cache/`
und prüft `quadriga-metadata.yml` dagegen. Schlägt die Validierung fehl, bricht
die GitHub Action `update-metadata.yml` ab, sodass keine fehlerhaften Metadaten
veröffentlicht werden. Zusätzlich erlaubt der oben beschriebene
`yaml-language-server`-Kommentar eine Prüfung direkt im Editor.

(technologie:metadaten:export-formate)=

## Metadaten-Exportformate

Die in `quadriga-metadata.yml` erfassten Metadaten werden automatisch in
verschiedene standardisierte Formate exportiert, um die Auffindbarkeit,
Nachnutzbarkeit und Interoperabilität der OER zu gewährleisten. Die
Transformation erfolgt durch Python-Skripte im Verzeichnis
`quadriga/metadata/` und wird im Build-Prozess automatisch ausgeführt.

### Generierte Formate

(technologie:metadaten:json-ld)=

#### JSON-LD (`quadriga-metadata.jsonld`)

<a href="https://json-ld.org" target="_blank" class="external-link">JSON-LD
(JavaScript Object Notation for Linked Data)</a> ist ein Format für
strukturierte, verlinkte Daten im Web. Die exportierten Metadaten enthalten
Aussagen in mehreren Vokabularen (u. a. schema.org, Dublin Core, LRMI). Die
Generierung erfolgt in `create_jsonld.py`.

Im Publikationsprozess werden per GitHub Action zusätzlich <a
    href="https://ogp.me" target="_blank" class="external-link">OpenGraph</a>-Tags,
JSON-LD-Blöcke und `<link>`-Verweise in die Startseite des Buchs sowie die
Kapitel-Startseiten integriert (`inject_all_metadata.py`).

(technologie:metadaten:rdf)=

#### RDF/XML (`quadriga-metadata.rdf`)

<a href="https://www.w3.org/RDF/" target="_blank" class="external-link">RDF
(Resource Description Framework)</a> in XML-Serialisierung ermöglicht die
Verarbeitung der Metadaten durch Semantic-Web-Anwendungen und Triple Stores. Die
Generierung erfolgt in `create_rdfxml.py`.

(technologie:metadaten:oersi)=

#### OERSI-Metadaten (`metadata.yml`)

Über den <a href="https://oersi.org" target="_blank"
class="external-link">OERSI (Open Educational Resources Search Index)</a> werden
OER auffindbar, indem Repositorien über eine Datei `metadata.yml` im
Wurzelverzeichnis erschlossen werden. Diese Datei verwendet
schema.org-/LRMI-Eigenschaften und wird in `create_oersi_metadata.py` aus
`quadriga-metadata.yml` erzeugt. Dabei werden die kontrollierten Vokabulare des
Application Profiles auf die von OERSI erwarteten Vokabulare abgebildet, bspw.
`disciplineLIST` auf die KIM-Hochschulfächersystematik und `targetGroupLIST` auf
die KIM-Bildungsstufe.

(technologie:metadaten:citation-cff)=

#### CITATION.cff und CITATION.bib

`CITATION.cff` ist der GitHub-Standard für die Zitation von Software und
Datensätzen (<a href="https://citation-file-format.github.io" target="_blank"
    class="external-link">Citation File Format</a>) und wird von GitHub genutzt,
um Zitationsempfehlungen anzuzeigen. Ergänzend wird mit `CITATION.bib` eine
BibTeX-Variante erzeugt. Beide Dateien werden bei jedem Lauf vollständig neu
geschrieben (`create_citation_cff.py`, `create_bibtex.py`); manuelle Änderungen
gehen verloren.

(technologie:metadaten:zenodo)=

#### Zenodo JSON (`.zenodo.json`)

Metadaten im Zenodo-Format für die Archivierung und DOI-Vergabe über die
Zenodo-Plattform. Diese Metadaten liefern die Grundlage für den Zenodo-Eintrag
(`create_zenodo_json.py`). Das Format ist definiert in <a
    href="https://github.com/zenodo/zenodo/blob/482ee72ad501cbbd7f8ce8df9b393c130d1970f7/zenodo/modules/deposit/jsonschemas/deposits/records/legacyrecord.json"
    target="_blank" class="external-link">`legacyrecord.json`</a>.

### Metadaten-Verarbeitungspipeline

Die Verarbeitung der Metadaten erfolgt in folgenden Schritten:

1. **Quelldateien**: `quadriga-metadata.yml` mit QUADRIGA Application Profile
   (siehe {ref}`schemaVersion <metadata:schema-version>`) sowie `_config.yml`,
   `_toc.yml` und die Lernzieldefinitionen in den `Lernziele.md`-Dateien der
   Kapitel.
1. **Lernziele**: `extract_from_lernziele.py` übernimmt Lernziele aus den
   `Lernziele.md`-Dateien in `quadriga-metadata.yml`.
1. **Validierung**: `validate_schema.py` prüft `quadriga-metadata.yml` gegen das
   JSON-Schema der Version 2.0.0.
1. **Abgleich mit dem Buch**: `extract_from_book_config.py` aktualisiert
   Informationen wie den Titel des Buchs und das Inhaltsverzeichnis auf Basis
   der Jupyter-Book-Konfigurationsdateien.
1. **Generierung**: Weitere Python-Skripte in `quadriga/metadata/`
   transformieren die YAML-Daten:
    - `create_citation_cff.py` → `CITATION.cff`
    - `create_bibtex.py` → `CITATION.bib`
    - `create_zenodo_json.py` → `.zenodo.json`
    - `create_jsonld.py` → `quadriga-metadata.jsonld`
    - `create_rdfxml.py` → `quadriga-metadata.rdf`
    - `create_oersi_metadata.py` → `metadata.yml`
1. **Versionierung**: Wird ein Versions-Tag (bspw. `v0.1.2`) gepusht, so
   aktualisiert `update_version_from_tag.py` die Felder
   {ref}`version <metadata:version>` und
   {ref}`dateModified <metadata:date-modified>`.
1. **Build**: Jupyter Book erstellt die HTML-Ausgabe in `_build/html/`.
1. **Injektion**: `inject_all_metadata.py` bettet OpenGraph- und
   JSON-LD-Daten in die HTML-Seiten ein und fügt Verweise auf die
   Metadatendateien hinzu.
1. **Bereitstellung**: `quadriga-metadata.jsonld` und `quadriga-metadata.rdf`
   werden in das Build-Verzeichnis kopiert.

Die Skripte nutzen gemeinsame Hilfsfunktionen aus `utils.py` für
YAML-Verarbeitung, Keyword-Extraktion und Formatierung. Die GitHub Action
`update-metadata.yml` startet bei jedem Push (oder manuell ausgelöst)
`run_all.py`, das die Metadatenskripte nacheinander ausführt. Ändert sich dabei
eine generierte Metadatendatei, committet die Action die Änderung automatisch
zurück in den Branch.

(technologie:metadaten:migration)=

## Migration von Version 1.0.0

Dateien nach Version 1.0.0 werden vom aktuellen Build-Prozess nicht mehr
akzeptiert. Die wichtigsten Änderungen im Überblick:

| Version 1.0.0 | Version 2.0.0 |
| --- | --- |
| Datei `metadata.yml` | Datei `quadriga-metadata.yml` |
| `authors` | `authorLIST` |
| `keywords` | `keywordLIST` |
| `table-of-contents` | `tableOfContents` |
| `discipline` | `disciplineLIST` |
| `research-object-type` | `researchObjectTypeLIST` |
| `target-group` | `targetGroupLIST` |
| `time-required` | `timeRequired` |
| `contributors` | `contributorLIST` (jetzt optional) |
| `git` | `identifierGit` |
| `url` | `identifierOER` |
| `prerequisites` | `prerequisiteLIST` |
| `used-tools` | `usedToolLIST` |
| `chapters` | `chapterLIST` |
| `date-issued` | `dateIssued` |
| `date-modified` | `dateModified` |
| `context-of-creation` | `contextOfCreation` |
| `quality-assurance` | `qualityAssurance` |
| `learning-resource-type` | `learningResourceType` |
| `schema-version` | `schemaVersion` (Wert `2.0.0`) |
| `license.content` | `license` (nur URL) |
| `license.code` | `licenseCode` |
| `given-names` / `family-names` | `givenName` / `familyName` |
| `credit` (Rollenobjekte) | `creditLIST` (Rollen als Text) |
| `learning-objectives` | `learningObjectiveLIST` |
| `learning-objective` | `description` |
| `data-flow` / `blooms-category` | `dataFlow` / `bloomsCategory` |
| `learning-goal` | `learningGoal` |
| `supplemented-by` | `supplementalMaterialLIST` (`title`/`url`) |

Felder wie `has-predecessor`, `has-successor` und `related-works`, die in
älteren Fassungen dieses Kapitels beschrieben waren, sind im Application Profile
2.0.0 nicht vorgesehen. Verweise auf verwandte OERs werden stattdessen über die
Felder `identifier` und `identifierOER` der jeweiligen OER sowie ggf. über
`supplementalMaterialLIST` abgebildet.

Für die Umstellung stellt das Repositorium ein Skript bereit, das eine
v1-Datei weitgehend automatisch konvertiert:

```bash
$ uv run convert-metadata-v1-to-v2.py -i metadata.yml -o quadriga-metadata.yml
```

Das Skript gibt Warnungen für Informationen aus, die nicht verlustfrei
übernommen werden können (bspw. `supplemented-by`-Einträge ohne URL). Prüfen Sie
die konvertierte Datei anschließend sorgfältig im Editor und ergänzen Sie
insbesondere `licenseCode`, falls die OER Programmcode enthält.
