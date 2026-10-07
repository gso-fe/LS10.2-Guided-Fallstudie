**HTML/CSS/Bootstrap-Konzepte — Referenz · Web-UI-Prototyping · LS10.2**

> Nachschlagewerk zu den Basis-Themen aus HTML, CSS und Bootstrap: Zu jedem Konzept die Fundstelle in der
> Fallstudie (`prototyp/`, wo vorhanden) und ein bis zwei vertiefende Links zum Mozilla Developer Network
> (MDN) bzw. zur Bootstrap-Dokumentation. Klappen Sie ein Konzept auf, wenn Sie es nachschlagen oder
> vertiefen wollen — die Reihenfolge der Abschnitte folgt dem Aufbau von HTML und CSS, nicht notwendigerweise
> Ihrer eigenen Arbeitsreihenfolge.
>
> Nicht jedes Konzept kommt in der Fallstudie vor — sie zeigt bewusst nur die *interessanten* Zustände, kein
> vollständiges Element-Lexikon. Wo eine Fundstelle fehlt, steht das hier offen so, mit einem MDN-Link als
> Ersatz.

## HTML – Struktur & Bausteine

<details>
<summary><strong>Grundgerüst und <code>&lt;meta&gt;</code> im <code>&lt;head&gt;</code></strong></summary>

**Fallstudie** (`index.html`):

```html
<!doctype html>
<html lang="de">
  <head>
    <meta charset="utf-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1" />
    <title>Offene Nachweise – Ausbilder</title>
    <link rel="stylesheet" href="vendor/bootstrap.min.css" />
    <link rel="stylesheet" href="css/styles.css" />
  </head>
```

Ohne das zweite `<meta>` (`viewport`) würde die Seite auf dem Smartphone wie eine verkleinerte Desktop-Seite
dargestellt — Mobile-First (siehe `howto_responsive-strategie.md`) greift dann nicht. `charset="utf-8"` steht
immer als Erstes im `<head>`, damit Umlaute und Sonderzeichen in der Datei richtig gelesen werden, bevor der
Browser weiterliest.

**Vertiefend (MDN):**
- [`<meta>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Elements/meta)
- [`<meta name="viewport">`](https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Elements/meta/name/viewport)

*(Kriterium 3 — Grundniveau)*

</details>

<details>
<summary><strong>Semantische Struktur (<code>header</code>, <code>nav</code>, <code>main</code>, <code>footer</code>, <code>section</code>, <code>article</code>)</strong></summary>

**Fallstudie** (`detail.html`, drei Ausschnitte):

```html
<header>
  <nav class="navbar bg-body-tertiary border-bottom">
    <div class="container">
      <a class="navbar-brand" href="../index.html">Berichtsheft-App</a>
      <span class="navbar-text">Ausbilder-Ansicht · K. Tari</span>
    </div>
  </nav>
</header>
```
```html
<main class="container py-4">
```
```html
<footer class="container py-4 text-muted border-top">
  <small>Fallstudie · Zustand: Detail (Standard)</small>
</footer>
```

`header`, `nav`, `main` und `footer` grenzen die Fallstudie klar gegen eine „div-Suppe" ab: Wer einen
Screenreader nutzt, kann direkt zur Hauptnavigation oder zum Hauptinhalt springen, ohne sich durch
verschachtelte `div`s zu tasten.

`section` und `article` kommen in der Fallstudie **nicht vor** — ihr Inhalt (eine Liste, ein Formular) bildet
keinen in sich abgeschlossenen Abschnitt im Sinne dieser Elemente. Für einen eigenen, zweispaltigen Screen
(Hauptinhalt + Nebeninhalt) wäre ein `<section>`/`<aside>`-Paar ein passender Ausgangspunkt.

**Vertiefend (MDN):**
- [`<header>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Elements/header) ·
  [`<nav>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Elements/nav) ·
  [`<main>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Elements/main) ·
  [`<footer>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Elements/footer)
- [`<section>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Elements/section) ·
  [`<article>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Elements/article)

*(Kriterium 3 — Grundniveau/Erweitert)*

</details>

<details>
<summary><strong>Überschriften-Hierarchie (<code>h1</code>–<code>h6</code>)</strong></summary>

**Fallstudie** (`index.html`):

```html
<h1 class="h4 mb-0 me-auto">Offene Ausbildungsnachweise</h1>
```

Auffällig: Das Element ist `<h1>` (die Überschrift der Seite — wichtig für Struktur und Screenreader), die
Klasse `h4` kommt zusätzlich von Bootstrap und ändert nur die *Schriftgröße*. Element und Klasse lösen zwei
verschiedene Dinge: `<h1>` die Bedeutung, `.h4` die Optik. Verkleinern Sie eine Überschrift nie, indem Sie
`<h1>` durch `<h4>` ersetzen — das würde die Struktur verändern, nicht nur das Aussehen.

**Vertiefend (MDN):**
- [`<h1>`–`<h6>`: Überschriften-Elemente](https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Elements/Heading_Elements)

*(Kriterium 3 — Grundniveau)*

</details>

<details>
<summary><strong>Fließtext: <code>p</code>, <code>strong</code>/<code>em</code>, <code>ul</code>/<code>ol</code>/<code>li</code></strong></summary>

**Fallstudie** (`zurueckweisen.html`):

```html
<p class="text-muted mb-3">José Schmidt-Da Silva · Woche 06.02.–12.02.</p>
```

und (`signiert.html`):

```html
<strong>Nachweis signiert.</strong> José Schmidt-Da Silva wurde informiert.
```

`em` sowie Listen (`ul`/`ol`/`li`) kommen in der Fallstudie **nicht vor** — die einzige listenartige Stelle
(die Nachweis-Übersicht) ist als Bootstrap-`list-group` aus `<div>`/`<a>`-Elementen gebaut, nicht als `<ul>`.
Das ist eine bewusste Bootstrap-Entscheidung (die Zeilen sollen klickbare Links sein, keine reinen
Listenpunkte) — für eigene Aufzählungen in Ihrem Flow ist `<ul>`/`<ol>` trotzdem meist die richtige Wahl.

**Vertiefend (MDN):**
- [`<p>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Elements/p) ·
  [`<strong>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Elements/strong) ·
  [`<em>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Elements/em)
- [`<ul>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Elements/ul) ·
  [`<ol>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Elements/ol) ·
  [`<li>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Elements/li)

*(Kriterium 3 — Grundniveau)*

</details>

<details>
<summary><strong>Links <code>&lt;a href&gt;</code> als Klickdummy-Navigation</strong></summary>

**Fallstudie** (`index.html`):

```html
<a href="zustaende/detail.html" class="list-group-item list-group-item-action active" aria-current="true">
  ...
</a>
```

Jeder Zustand der Fallstudie ist eine eigene, über `href` verlinkte Seite — der komplette Klickdummy kommt
ohne eine einzige Zeile JavaScript aus. `aria-current="true"` zeigt zusätzlich an, welcher Eintrag gerade
aktiv ist (mehr dazu in `howto_ui-zustaende.md`, Abschnitt ARIA).

**Vertiefend (MDN):**
- [`<a>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Elements/a)

*(ohne direkten Bewertungsbezug — trägt den gesamten Klickdummy)*

</details>

<details>
<summary><strong>Bilder <code>&lt;img&gt;</code> mit <code>alt</code></strong></summary>

**Kommt in der Fallstudie nicht vor** — kein einziges `<img>` in `prototyp/`. Setzen Sie `<img>`
in Ihrem eigenen Flow ein (z. B. ein Logo oder ein Profilbild) und denken Sie an den `alt`-Text: Er muss den
*Inhalt* des Bildes in Worten wiedergeben, nicht nur „Bild" oder den Dateinamen.

**Vertiefend (MDN):**
- [`<img>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Elements/img)

*(Kriterium 3 bzw. 7 — Barrierefreiheit)*

</details>

<details>
<summary><strong><code>div</code>/<code>span</code> — und bewusst keine div-Suppe</strong></summary>

**Fallstudie** (`index.html`, zur Lesbarkeit neu eingerückt):

```html
<div class="d-flex w-100 justify-content-between align-items-center">
  <strong>José Schmidt-Da Silva</strong>
  <span class="badge text-bg-primary">eingereicht</span>
</div>
```

`div` ist block-, `span` ist inline-artig — deshalb steht der Name nicht in einem eigenen Block, sondern bleibt
mit dem Badge in einer Zeile. Beide Elemente tragen für sich genommen keine Bedeutung; sie existieren nur, um
eine Bootstrap-Klasse anzuhängen. Wo ein semantisches Element passt (`header`, `nav`, `button` …), hat es laut
Themenkatalog Vorrang vor `div`/`span`.

**Vertiefend (MDN):**
- [`<div>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Elements/div) ·
  [`<span>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Elements/span)

*(Kriterium 3 — Grundniveau/Erweitert)*

</details>

<details>
<summary><strong><code>id</code>- vs. <code>class</code>-Attribut</strong></summary>

**Fallstudie** (`zurueckweisen.html`):

```html
<textarea class="form-control is-invalid" id="kommentar" name="kommentar" rows="4" aria-invalid="true"
          required aria-describedby="kommentarHilfe kommentarFehler"></textarea>
<div id="kommentarFehler" class="invalid-feedback">
  ...
</div>
```

`id="kommentar"` ist eindeutig (genau ein Element im Dokument) und wird hier nicht für CSS, sondern als
Sprungziel für `aria-describedby` genutzt — der Screenreader liest den damit verknüpften Text vor. `class`
dagegen ist mehrfach vergebbar und steuert hier über Bootstrap das Aussehen (`form-control`, `is-invalid`).
Merkregel: **eine `id` pro Element, `class` für alles, was mehrfach vorkommen darf.**

**Vertiefend (MDN):**
- [`id`](https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Global_attributes/id) ·
  [`class`](https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Global_attributes/class)

*(Kriterium 4 — Grundniveau)*

</details>

## HTML – Formulare

<details>
<summary><strong><code>&lt;form&gt;</code> (<code>action</code>/<code>method</code> konzeptionell)</strong></summary>

**Fallstudie** (`zurueckweisen.html`):

```html
<form action="#" method="post" novalidate>
  ...
</form>
```

`action="#"` ist ein Platzhalter — die Fallstudie sendet nichts wirklich ab, es gibt ja keinen Server dahinter.
Trotzdem gehören `action` (wohin die Daten gingen) und `method` (wie, hier `post`) konzeptionell zu jedem
Formular. `novalidate` unterdrückt hier bewusst nur die Fehlerblase des Browsers beim Absenden, nicht die
Validierung selbst (siehe `howto_ui-zustaende.md`, Abschnitt Validierungs-Zustände).

**Vertiefend (MDN):**
- [`<form>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Elements/form)

*(Kriterium 3 — Grundniveau)*

</details>

<details>
<summary><strong><code>&lt;label for&gt;</code> ↔ Input-Zuordnung</strong></summary>

**Fallstudie** (`zurueckweisen.html`):

```html
<label for="kommentar" class="form-label">Grund der Zurückweisung</label>
<textarea class="form-control is-invalid" id="kommentar" ...></textarea>
```

`for="kommentar"` verweist auf `id="kommentar"` — ein Klick auf den Label-Text setzt den Fokus ins Feld, und
ein Screenreader liest „Grund der Zurückweisung" als Namen des Feldes vor. Ohne diese Zuordnung wäre das Label
nur optisch in der Nähe des Feldes, fachlich aber nicht verbunden — einer der häufigsten a11y-Fehler.

**Vertiefend (MDN):**
- [`<label>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Elements/label)

*(Kriterium 3 — Grundniveau)*

</details>

<details>
<summary><strong>Input-Typen (<code>text</code>, <code>email</code>, <code>password</code>, <code>number</code>, <code>date</code>)</strong></summary>

**Kommt in der Fallstudie nicht vor** — das einzige Eingabeelement ist ein `<textarea>` (Freitext), kein
`<input>`. Für Ihren eigenen Flow (z. B. ein Login mit Benutzername/Passwort oder ein Tageseintrag mit Datum)
wählen Sie den `type` passend zur Art der Eingabe — das liefert auf dem Smartphone automatisch die passende
Tastatur (z. B. Ziffernblock bei `type="number"`).

**Vertiefend (MDN):**
- [`<input>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Elements/input)

*(Kriterium 3 — Grundniveau)*

</details>

<details>
<summary><strong>Input-Attribute: <code>required</code>, <code>disabled</code>, <code>readonly</code>, <code>min</code>/<code>max</code>, <code>pattern</code>, <code>placeholder</code></strong></summary>

**Fallstudie** (`zurueckweisen.html`):

```html
<textarea class="form-control is-invalid" id="kommentar" name="kommentar" rows="4" aria-invalid="true"
          required aria-describedby="kommentarHilfe kommentarFehler"></textarea>
```

und (`signiert.html`):

```html
<button type="button" class="btn btn-success" disabled aria-describedby="signiertHinweis">
  Signieren
</button>
```

`required` und `disabled` sind hier keine reine Formular-Deko, sondern bereits **UI-States**: Ein leeres
Pflichtfeld ist automatisch `:invalid` (siehe `howto_ui-zustaende.md`), ein deaktivierter Button verschwindet
aus der Tab-Reihenfolge. `readonly`, `min`/`max`, `pattern` und `placeholder` nutzt die Fallstudie nicht — alle
vier sind auf der MDN-Seite des jeweiligen Elements mit Beispiel dokumentiert.

**Vertiefend (MDN):**
- [`required`](https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Attributes/required) ·
  [`disabled`](https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Attributes/disabled)

*(Kriterium 3 — Grundniveau; `disabled` zusätzlich Kriterium 5)*

</details>

<details>
<summary><strong><code>&lt;textarea&gt;</code></strong></summary>

**Fallstudie** (`zurueckweisen.html`):

```html
<textarea class="form-control is-invalid" id="kommentar" name="kommentar" rows="4" aria-invalid="true"
          required aria-describedby="kommentarHilfe kommentarFehler"></textarea>
```

`rows="4"` legt nur die anfängliche Höhe fest — anders als bei `<input>` kann die Nutzer\*in ein `<textarea>`
in den meisten Browsern zusätzlich selbst in der Höhe ziehen.

**Vertiefend (MDN):**
- [`<textarea>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Elements/textarea)

*(Kriterium 3 — Grundniveau)*

</details>

<details>
<summary><strong><code>&lt;select&gt;</code>/<code>&lt;option&gt;</code></strong></summary>

**Kommt in der Fallstudie nicht vor.** Denkbar wäre es z. B. für die Abteilungsauswahl im
Tageseintrag-Formular (Flow C) oder die Anrede im Login (Flow A) — überall dort, wo aus einer festen,
bekannten Liste **genau eine** Option gewählt wird.

**Vertiefend (MDN):**
- [`<select>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Elements/select) ·
  [`<option>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Elements/option)

*(Kriterium 3 — Grundniveau)*

</details>

<details>
<summary><strong>Checkbox / Radio</strong></summary>

**Kommt in der Fallstudie nicht vor.** Checkbox und Radio unterscheiden sich darin, wie viele Optionen
gleichzeitig gewählt werden dürfen: **Radio** = genau eine aus einer Gruppe (gleicher `name`), **Checkbox** =
beliebig viele unabhängig voneinander. Beide lassen sich über die Pseudoklasse `:checked` rein in CSS stylen —
Grundlage der „CSS-only"-Tricks aus dem Themenkatalog.

**Vertiefend (MDN):**
- [`<input type="checkbox">`](https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Elements/input/checkbox) ·
  [`<input type="radio">`](https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Elements/input/radio)

*(Kriterium 3 — Grundniveau)*

</details>

<details>
<summary><strong><code>&lt;button&gt;</code> (<code>submit</code>/<code>button</code>)</strong></summary>

**Fallstudie** (`zurueckweisen.html`):

```html
<button type="submit" class="btn btn-danger">Zurückweisen senden</button>
```

und (`signiert.html`):

```html
<button type="button" class="btn btn-success" disabled aria-describedby="signiertHinweis">
  Signieren
</button>
```

Der Unterschied ist nicht nur Geschmack: `type="submit"` löst das Absenden des umgebenden `<form>` aus,
`type="button"` tut von sich aus **nichts** — hier bewusst gewählt, weil der „Signieren"-Button in diesem
Zustand sowieso `disabled` ist und zu keinem Formular gehört. Ein `<button>` ohne explizites `type` ist
innerhalb eines Formulars automatisch `submit` — eine häufige Fehlerquelle.

**Vertiefend (MDN):**
- [`<button>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Elements/button)

*(Kriterium 3 — Grundniveau)*

</details>

## CSS – Grundlagen

<details>
<summary><strong>CSS einbinden (inline / intern / extern <code>&lt;link&gt;</code>)</strong></summary>

**Fallstudie** (`index.html`):

```html
<link rel="stylesheet" href="vendor/bootstrap.min.css" />
<link rel="stylesheet" href="css/styles.css" />
```

Beide Stylesheets sind **extern** eingebunden — eines für Bootstrap, eines für die eigenen, wenigen Ergänzungen.
So lädt jede der sechs Zustandsseiten dieselben Regeln, ohne sie zu wiederholen: Eine Änderung in `styles.css`
wirkt sofort überall. **Inline** (`style="…"` direkt am Element) und **intern** (`<style>` im `<head>`) kommen
in der Fallstudie nicht vor — beide sind für schnelle Experimente nützlich, aber nicht für fertiges Material:
Inline-Styles lassen sich nicht wiederverwenden und übertrumpfen in der Kaskade fast alles andere.

**Vertiefend (MDN):**
- [`<link rel="stylesheet">`](https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Elements/link) ·
  [`<style>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Elements/style) ·
  [`style`-Attribut](https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Global_attributes/style)

*(Kriterium 4 — Grundniveau)*

</details>

<details>
<summary><strong>Selektoren: Element / Klasse / ID / Nachfahre / Gruppierung</strong></summary>

**Fallstudie** (`css/styles.css`):

```css
:focus-visible {
  outline: 3px solid #1d4ed8;
  outline-offset: 2px;
}

.detail-pane { position: sticky; top: 1rem; }
```

Das eigene Stylesheet ist bewusst klein (zwei aktive Regeln) — es überschreibt Bootstrap nur gezielt, nicht
grundsätzlich. Gezeigt sind hier ein Pseudoklassen- und ein Klassen-Selektor; einen reinen ID-Selektor,
einen Nachfahre-Selektor (`.a .b`) oder eine Gruppierung (`.a, .b`) brauchte die Fallstudie bisher nicht. Alle
drei stecken aber in jeder Bootstrap-Regel — nur eben minifiziert in `vendor/bootstrap.min.css` und darum als
Lernquelle kaum geeignet. Besser: ein beliebiges Bootstrap-Element in den DevTools inspizieren und dort
nachsehen, welcher Selektor gerade greift.

**Vertiefend (MDN):**
- [Klassen-Selektoren](https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Selectors/Class_selectors)

*(Kriterium 4 — Grundniveau)*

</details>

<details>
<summary><strong>Box-Modell (<code>content</code>/<code>padding</code>/<code>border</code>/<code>margin</code>, <code>box-sizing</code>)</strong></summary>

**Kein eigener Codeauszug** — das Box-Modell steckt in jedem Element, auch wenn es niemand explizit
hinschreibt. Am besten direkt in den DevTools nachvollziehen: Ein Bootstrap-Element wie `.card-body`
anklicken und die Box-Modell-Ansicht öffnen (Kriterium 4, „schaltet in den DevTools einen Zustand ein" setzt
genau diese Fähigkeit voraus).

**Vertiefend (MDN):**
- [Das Box-Modell](https://developer.mozilla.org/en-US/docs/Learn_web_development/Core/Styling_basics/Box_model)

*(Kriterium 4 — Grundniveau)*

</details>

<details>
<summary><strong>State-Pseudoklassen <code>:hover</code> <code>:focus</code> <code>:focus-visible</code> <code>:active</code> <code>:disabled</code> <code>:checked</code> <code>:invalid</code></strong></summary>

**Fallstudie** (`css/styles.css`, aktive Regel):

```css
:focus-visible {
  outline: 3px solid #1d4ed8;
  outline-offset: 2px;
}
```

und (dieselbe Datei, bewusst **auskommentiert** als Alternative):

```css
/* .form-control:invalid                     { border-color: #dc3545; }
   .form-control:invalid ~ .invalid-feedback { display: block; } */
```

`:focus-visible` ist aktiv und sorgt für den sichtbaren Tastatur-Rahmen auf der ganzen Seite. Die
`:invalid`-Regel zeigt den **anderen** Weg zum Fehler-Zustand aus `zurueckweisen.html`: Statt der statischen
Bootstrap-Klasse `.is-invalid` (die immer rot ist, egal was im Feld steht) reagiert `:invalid` **dynamisch**
auf die native Validierung — deshalb hier bewusst als Kommentar, damit im Mockup die statische Variante aktiv
bleibt. `:hover`, `:active` und `:checked` kommen im eigenen CSS nicht vor; sie stecken in Bootstraps
Button- und Formular-Stilen und lassen sich dort in den DevTools beobachten.

**Vertiefend (MDN):**
- [`:focus-visible`](https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Selectors/:focus-visible) ·
  [`:invalid`](https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Selectors/:invalid)

*(Kriterium 4/5 — Grundniveau/Erweitert)*

</details>

<details>
<summary><strong>Farben &amp; Einheiten (<code>px</code>/<code>rem</code>/<code>%</code>, Farbwerte)</strong></summary>

**Fallstudie** (`css/styles.css`):

```css
:focus-visible {
  outline: 3px solid #1d4ed8;
  outline-offset: 2px;
}

@media (min-width: 992px) {
  .detail-pane { position: sticky; top: 1rem; }
}
```

`3px`/`2px` sind feste Pixelwerte — bewusst nur für die dünne Fokus-Outline, nicht fürs Layout (das Layout
übernehmen Bootstraps `rem`-/`%`-basierte Utilities). `1rem` skaliert mit der Schriftgrößen-Einstellung der
Nutzer\*in — wichtig für alle, die den Browser-Zoom oder eine größere Schrift eingestellt haben. `#1d4ed8`
ist ein sechsstelliger Hex-Farbwert (Rot/Grün/Blau).

**Vertiefend (MDN):**
- [Farbwerte (`<color>`)](https://developer.mozilla.org/en-US/docs/Web/CSS/color_value) ·
  [CSS-Werte und Einheiten](https://developer.mozilla.org/en-US/docs/Web/CSS/Guides/Values_and_units)

*(Kriterium 4 — Grundniveau)*

</details>

## CSS – Layout (Framework-first)

<details>
<summary><strong><code>display</code>: block / inline / inline-block</strong></summary>

**Kein eigener Codeauszug** — `display` wird in der Fallstudie nie direkt gesetzt, sondern über
Bootstrap-Klassen wie `.d-flex` gesteuert (siehe unten). Die native Grundfrage „Warum nimmt mein `<span>`
keine eigene Breite an, mein `<div>` aber schon?" (vgl. den Eintrag `div`/`span` oben) lässt sich am besten
direkt in den DevTools am Element nachvollziehen.

**Vertiefend (MDN):**
- [`display`](https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Properties/display)

*(Kriterium 4 — Grundniveau)*

</details>

<details>
<summary><strong>Bootstrap-Grid (<code>container</code>/<code>row</code>/<code>col</code> + Breakpoints)</strong></summary>

**Fallstudie** (`index.html`):

```html
<div class="row g-4">
  <div class="col-12 col-lg-5">
    <!-- Liste -->
  </div>
  <div class="col-12 col-lg-7 d-none d-lg-block">
    <!-- Detail -->
  </div>
</div>
```

Mobil (unter `lg`) ist jede Spalte `col-12` — volle Breite, die Spalten stehen also untereinander: erst die
Liste, das Detail ist komplett ausgeblendet (`d-none`). Ab `lg` (≥ 992 px) teilen sich Liste und Detail die
Zeile im Verhältnis 5/7 (Master-Detail) — genau die „zweite Ebene", die Kriterium 2/6 auf Desktop verlangt.

**Vertiefend (Bootstrap-Dokumentation):**
- [Grid-System](https://getbootstrap.com/docs/5.3/layout/grid/) ·
  [Breakpoints](https://getbootstrap.com/docs/5.3/layout/breakpoints/)

*(Kriterium 6 — Grundniveau/Erweitert)*

</details>

<details>
<summary><strong>Bootstrap-Utilities (Spacing <code>m-</code>/<code>p-</code>, <code>d-flex</code>, <code>text-</code>/<code>bg-</code>)</strong></summary>

**Fallstudie** (`index.html`):

```html
<div class="d-flex flex-wrap align-items-center gap-2 mb-3">
  <h1 class="h4 mb-0 me-auto">Offene Ausbildungsnachweise</h1>
  <span class="badge text-bg-primary">eingereicht</span>
</div>
```

Keine der Klassen hier ist eigenes CSS: `d-flex` setzt `display: flex`, `gap-2`/`mb-3` setzen Abstände,
`text-bg-primary` setzt Text- und Hintergrundfarbe passend zueinander. Dieselbe Zeile ohne Bootstrap würde ein
eigenes Stylesheet mit mehreren Regeln brauchen.

**Vertiefend (Bootstrap-Dokumentation):**
- [Flexbox-Utilities](https://getbootstrap.com/docs/5.3/utilities/flex/) ·
  [Abstands-Utilities](https://getbootstrap.com/docs/5.3/utilities/spacing/)

*(Kriterium 4 — Grundniveau)*

</details>

<details>
<summary><strong>Bootstrap-Komponenten (<code>card</code>/<code>navbar</code>/<code>alert</code>/<code>badge</code>/<code>form-control</code>/<code>table</code>)</strong></summary>

**Fallstudie** (`signiert.html`):

```html
<div class="alert alert-success mt-2" role="status">
  <strong>Nachweis signiert.</strong> José Schmidt-Da Silva wurde informiert.
</div>
```

Alle sechs Komponenten kommen in der Fallstudie vor: `card` (`detail.html`), `navbar` (Kopfbereich jeder
Seite), `alert` (oben), `badge` (die Status-Markierungen „eingereicht"/„signiert"/„zurückgewiesen"),
`form-control` (`zurueckweisen.html`) und `table` (`detail.html`, die Tages-Tabelle). Jede liefert ihre
eigenen Zustands-Varianten mit (`alert-success`/`alert-danger`, `text-bg-primary`/`text-bg-success` …) — das
ist der pragmatische Weg zu den UI-States aus `howto_ui-zustaende.md`, ganz ohne eigenes CSS.

**Vertiefend (Bootstrap-Dokumentation):**
- [Card](https://getbootstrap.com/docs/5.3/components/card/) ·
  [Navbar](https://getbootstrap.com/docs/5.3/components/navbar/) ·
  [Alert](https://getbootstrap.com/docs/5.3/components/alerts/) ·
  [Badge](https://getbootstrap.com/docs/5.3/components/badge/) ·
  [Form Control](https://getbootstrap.com/docs/5.3/forms/form-control/) ·
  [Tabellen](https://getbootstrap.com/docs/5.3/content/tables/)

*(Kriterium 3/4 — Grundniveau)*

</details>

## CSS – Responsive Design

<details>
<summary><strong>Mobile-First-Denkweise</strong></summary>

**Fallstudie** (`index.html`, derselbe Ausschnitt wie beim Bootstrap-Grid):

```html
<div class="col-12 col-lg-5">...</div>
```

`col-12` gilt **immer**, `col-lg-5` kommt erst dazu, wenn der Bildschirm breit genug ist. Das ist Mobile-First
konkret: Die Basis-Regel gilt für den kleinsten Bildschirm, größere Bildschirme bekommen zusätzliche Regeln —
nicht umgekehrt. Die ausführliche Begründung (Progressive Enhancement vs. Graceful Degradation) steht in
`howto_responsive-strategie.md`.

**Vertiefend (Bootstrap-Dokumentation):**
- [Breakpoints](https://getbootstrap.com/docs/5.3/layout/breakpoints/)

*(Kriterium 6 — Grundniveau)*

</details>

<details>
<summary><strong>Framework-Breakpoints (<code>col-md-</code>, <code>d-none d-md-block</code>)</strong></summary>

**Fallstudie** (`index.html`):

```html
<p class="text-muted small d-lg-none">
  Tippen Sie einen Nachweis an, um ihn zu prüfen.
</p>
...
<div class="col-12 col-lg-7 d-none d-lg-block">
```

Zwei Seiten derselben Medaille: `d-lg-none` blendet den Hinweistext **ab** `lg` aus (er ist nur auf dem
Smartphone nötig, wo man einen Eintrag antippen muss); `d-none d-lg-block` blendet die Detailspalte **bis**
`lg` aus und zeigt sie erst ab Desktop-Breite. Beide nutzen denselben Breakpoint (`lg` = 992 px), nur mit
entgegengesetzter Richtung.

**Vertiefend (Bootstrap-Dokumentation):**
- [Breakpoints](https://getbootstrap.com/docs/5.3/layout/breakpoints/) ·
  [Display-Utilities](https://getbootstrap.com/docs/5.3/utilities/display/)

*(Kriterium 6 — Grundniveau)*

</details>

## JavaScript (bewusst minimal)

<details>
<summary><strong>Kein eigenes JS / Klickdummy über verlinkte Seiten</strong></summary>

**Fallstudie:** Keine einzige der sechs Seiten in `prototyp/` enthält ein `<script>`-Tag. Jeder
Zustand (leer, lädt, Fehler, signiert …) ist stattdessen eine eigene HTML-Datei, verlinkt über ganz normale
`<a href>`-Elemente (siehe den Eintrag „Links" oben). Das ist kein Behelf, sondern die bewusste Methode dieser
Lernsituation: Ein UI-Zustand lässt sich zeigen, ohne dass ihn eine Zeile Code *herstellt*.

Kein MDN-Link an dieser Stelle — es geht hier nicht um ein Web-Konzept, sondern um die Arbeitsweise dieser
Fallstudie selbst.

*(ohne direkten Bewertungsbezug — methodische Vorgabe der gesamten Einheit)*

</details>
