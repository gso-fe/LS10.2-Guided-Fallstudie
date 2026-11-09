**Kontrollfragen — Selbsttest zu HTML/CSS/Bootstrap, UI-Zuständen, Responsive & Barrierefreiheit ·
Web-UI-Prototyping · LS10.2**

> Fragen zur Selbstkontrolle der fachlichen Inhalte aus `guided-fallstudie.md`, `howto_ui-zustaende.md`,
> `howto_responsive-strategie.md` und `howto_barrierefreiheit.md` — unabhängig von den konkreten
> Bewertungskriterien und ohne Bezug auf die Fallstudien-Dateien selbst. Beantworten Sie die Frage zuerst
> selbst, bevor Sie die Lösung aufklappen.

## HTML/CSS/Bootstrap-Grundlagen

*(Fragen zu `guided-fallstudie.md`)*

<details>
<summary>Welches Element ist im <code>&lt;head&gt;</code> eines gültigen
HTML5-Dokuments das einzige echte Pflicht-Element?</summary>

`<title>`. `charset` sollte zwar ebenfalls so früh wie möglich stehen, ist aber kein Pflicht-Element im
selben Sinne — `<title>` ist das einzige Element, das ein gültiges HTML5-Dokument im `<head>` zwingend
benötigt.

</details>

<details>
<summary>Ein Kollege will eine Überschrift optisch verkleinern, indem er
<code>&lt;h1&gt;</code> durch <code>&lt;h4&gt;</code> ersetzt. Bewerten Sie diesen Vorschlag.</summary>

Der Vorschlag ist falsch. `<h1>` legt die *Bedeutung* fest (Dokumentstruktur, wichtig für Screenreader und
Suchmaschinen), nicht die Schriftgröße. Richtig wäre, `<h1>` als Element zu behalten und nur die *Optik*
über CSS zu ändern — z. B. über eine Klasse, die lediglich die Schriftgröße beeinflusst.

</details>

<details>
<summary>Was unterscheidet das <code>id</code>-Attribut grundsätzlich vom
<code>class</code>-Attribut?</summary>

`id` darf pro Dokument nur einmal vorkommen — sie adressiert ein einzelnes Element eindeutig (z. B. als
Sprungziel für `aria-describedby` oder `label[for]`). `class` darf beliebig oft vergeben werden und
gruppiert mehrere Elemente, meist für CSS- oder JavaScript-Zugriff.

</details>

<details>
<summary>Welches Attribut verbindet ein <code>&lt;label&gt;</code> fachlich mit
einem Eingabefeld?</summary>

Das Attribut `for` am `<label>`, das auf die `id` des zugehörigen Feldes verweist.

</details>

<details>
<summary>Was bewirkt das Attribut <code>required</code> an einem Eingabefeld, ganz
ohne eigenes JavaScript?</summary>

Der Browser führt automatisch eine native Validierung durch: Das Feld wird als `:invalid` markiert, solange
es leer ist, und das Formular lässt sich nicht absenden.

</details>

<details>
<summary>Nennen Sie die drei Arten, CSS in eine HTML-Seite einzubinden.</summary>

Inline (`style="…"` direkt am Element), intern (`<style>` im `<head>`), extern (`<link rel="stylesheet">`
auf eine separate Datei).

</details>

<details>
<summary>Warum ist eine inline-<code>style</code>-Angabe für ein fertiges Projekt
mit mehreren Seiten ungeeignet, auch wenn sie technisch funktioniert?</summary>

Inline-Styles lassen sich nicht wiederverwenden — eine Änderung müsste auf jeder Seite einzeln vorgenommen
werden — und sie überschreiben in der CSS-Kaskade durch ihre hohe Spezifität fast jede andere Regel, was
spätere Anpassungen zusätzlich erschwert.

</details>

<details>
<summary>Aus welchen vier Schichten besteht das CSS-Box-Modell, von innen nach
außen?</summary>

`content`, `padding`, `border`, `margin`.

</details>

<details>
<summary>Begründen Sie, warum der CSS-Ruhezustand eines Elements
(<code>default</code>) keine eigene Pseudoklasse besitzt.</summary>

`default` ist keine eigene, abfragbare Bedingung, sondern einfach das, was automatisch gilt, solange keine
spezifischere Regel (eine Pseudoklasse wie `:hover` oder ein Attribut-Selektor wie `[disabled]`) zutrifft —
die unqualifizierte Grundregel des Elements. Es gibt daher keinen Selektor, der ihn gezielt ansprechen
müsste.

</details>

<details>
<summary>Was unterscheidet eine Bootstrap-Utility-Klasse (z. B.
<code>d-flex</code>) von einer Bootstrap-Komponente (z. B. <code>card</code>)?</summary>

Eine Utility-Klasse setzt genau eine CSS-Eigenschaft. Eine Komponente ist ein vorgefertigter, aus mehreren
HTML-Elementen und Klassen zusammengesetzter UI-Baustein mit eigenem CSS und oft bereits enthaltenen
Zustandsvarianten.

</details>

<details>
<summary>Nennen Sie drei semantische HTML5-Elemente, die wiederkehrende Seitenbereiche gliedern, und
beschreiben Sie kurz deren Aufgabe.</summary>

Zum Beispiel: `header` (Kopfbereich, oft mit Navigation/Logo), `nav` (Navigationsblock), `main`
(Hauptinhalt der Seite), `footer` (Fußbereich). Diese Elemente tragen von sich aus keine eigene Optik,
geben aber Screenreadern und Suchmaschinen eine erkennbare Landmarken-Struktur der Seite.

</details>

<details>
<summary>Warum sollte eine Aufzählung in der Regel mit <code>&lt;ul&gt;</code>/<code>&lt;li&gt;</code>
ausgezeichnet werden statt mit mehreren <code>&lt;div&gt;</code>-Elementen?</summary>

`<ul>`/`<li>` tragen eine eigene Bedeutung — eine Aufzählung —, die ein Screenreader als solche ankündigt
und durch die sich gezielt navigieren lässt. `<div>` ist dagegen bedeutungslos und liefert diese
Information nicht.

</details>

<details>
<summary>Was muss ein <code>alt</code>-Attribut inhaltlich leisten, und wann ist ein bewusst leeres
<code>alt=""</code> die richtige Lösung?</summary>

Der `alt`-Text muss den *Inhalt* des Bildes in Worten wiedergeben, nicht nur „Bild" oder den Dateinamen.
Ein bewusst leeres `alt=""` ist richtig, wenn das Bild rein dekorativ ist und keinen eigenen
Informationswert hat.

</details>

<details>
<summary>Nennen Sie drei typische <code>&lt;input&gt;</code>-Typen und beschreiben Sie jeweils den
praktischen Vorteil gegenüber <code>type="text"</code>.</summary>

Zum Beispiel: `email` (grobe Formatprüfung, auf Mobilgeräten eine passende Tastatur mit „@"-Taste),
`password` (verdeckt die Eingabe), `number` (Ziffernblock auf dem Smartphone, erlaubt `min`/`max`), `date`
(liefert einen nativen Datumspicker).

</details>

<details>
<summary>Was unterscheidet <code>&lt;textarea&gt;</code> von <code>&lt;input type="text"&gt;</code>?</summary>

`<textarea>` ist für mehrzeiligen Freitext gedacht und lässt sich in den meisten Browsern zusätzlich in der
Höhe ziehen. Es kennt kein `type`-Attribut, da es von sich aus bereits auf genau einen Zweck festgelegt
ist.

</details>

<details>
<summary>Wann ist ein <code>&lt;select&gt;</code>-Element die bessere Wahl gegenüber mehreren
Radio-Buttons?</summary>

Wenn aus einer längeren, festen, bekannten Liste genau eine Option gewählt werden soll — ein Dropdown
nimmt dabei deutlich weniger Platz ein als eine vollständig ausgeklappte Liste von Radio-Buttons.

</details>

<details>
<summary>Was unterscheidet eine Checkbox grundsätzlich von einem Radio-Button?</summary>

Radio-Buttons erlauben genau eine Auswahl aus einer Gruppe mit gleichem `name`; Checkboxen erlauben
beliebig viele unabhängige Auswahlen.

</details>

<details>
<summary>Welchen Unterschied macht das Attribut <code>type</code> an einem <code>&lt;button&gt;</code>
innerhalb eines Formulars — und was passiert, wenn man es weglässt?</summary>

`type="submit"` löst das Absenden des umgebenden Formulars aus, `type="button"` tut von sich aus nichts.
Lässt man `type` weg, ist ein `<button>` innerhalb eines Formulars automatisch `submit` — eine häufige
Fehlerquelle.

</details>

<details>
<summary>Nennen Sie drei CSS-Pseudoklassen, die einen UI-Zustand ansprechen, und beschreiben Sie kurz,
wann sie jeweils greifen.</summary>

Zum Beispiel: `:hover` (die Maus befindet sich über dem Element), `:focus` (das Element ist per Tastatur
oder Klick fokussiert), `:disabled` (das Element ist deaktiviert), `:invalid` (die aktuelle Eingabe erfüllt
die Validierung nicht).

</details>

<details>
<summary>Was unterscheidet die Einheit <code>rem</code> von <code>px</code>, und warum ist
<code>rem</code> oft die zugänglichere Wahl?</summary>

`px` ist ein absoluter, fester Wert. `rem` ist relativ zur Schriftgrößen-Einstellung und skaliert daher
mit, wenn jemand den Browser-Zoom oder eine größere Schrift eingestellt hat.

</details>

## UI-Zustände

*(Fragen zu `howto_ui-zustaende.md`)*

<details>
<summary>Nennen Sie die drei Auslöser, aus denen sich der Zustand eines
UI-Elements ändern kann.</summary>

Interaktion (reagiert das Element unmittelbar auf eine Nutzerhandlung?), Daten/Prozess (hängt der Zustand
von einer Phase eines Vorgangs der Anwendung ab?), Validierung (wird eine Eingabe gegen fachliche
Anforderungen geprüft?).

</details>

<details>
<summary>Welche Interaktions-Zustände durchläuft ein Button typischerweise, ausgehend
vom Ruhezustand?</summary>

`default` → `hover` → `focus` → `active`, und zusätzlich `disabled`, wenn er nicht bedienbar sein soll.

</details>

<details>
<summary>Ein Absenden-Button wird beim Klick deaktiviert und zeigt zugleich einen
Lade-Spinner. Welche Auslöser wirken hier zusammen, und wie sollten Sie das in einem Zustandsdiagramm
vermerken?</summary>

Es kombinieren sich ein Interaktions-Auslöser (`disabled`) und ein Daten-/Prozess-Auslöser (`lädt`) an ein
und demselben Element. Im Zustandsdiagramm hält man das am besten nicht als mehrere isolierte
Einzelzustände fest, sondern als Kombination zweier unabhängiger Auslöser an derselben Stelle.

</details>

<details>
<summary>Was unterscheidet Daten-/Prozess-Zustände grundsätzlich von
Interaktions-Zuständen?</summary>

Bei Interaktions-Zuständen entscheidet die Nutzer\*in unmittelbar (Hover, Klick). Bei
Daten-/Prozess-Zuständen entscheidet die Anwendung selbst, in welcher Phase eines Vorgangs (z. B. Laden,
Absenden) sie sich gerade befindet.

</details>

<details>
<summary>Nennen Sie je einen Vor- und Nachteil der statischen Bootstrap-Klasse
<code>.is-invalid</code> gegenüber der dynamischen Pseudoklasse <code>:invalid</code>.</summary>

`.is-invalid` (statisch) zeigt den Zustand unabhängig vom tatsächlichen Feldinhalt, bis die Klasse aktiv
entfernt wird — nützlich, um einen Zustand gezielt zu erzwingen, z. B. in einem Mockup. `:invalid`
(dynamisch) reagiert automatisch auf die native Validierung und bleibt immer aktuell, lässt sich aber nicht
unabhängig vom tatsächlichen Feldinhalt erzwingen.

</details>

<details>
<summary>Was liest ein Screenreader für ein fokussiertes Element im Kern vor, und in
welcher Reihenfolge?</summary>

Name, Rolle, Zustand und optional eine Beschreibung — in dieser Reihenfolge.

</details>

<details>
<summary>Warum darf ein Statuswechsel (z. B. „gültig"/„ungültig") niemals
ausschließlich über Farbe kommuniziert werden? Nennen Sie eine alternative Umsetzung.</summary>

Farbe allein ist für farbenblinde oder nicht-sehende Nutzer\*innen nicht wahrnehmbar bzw. nicht
unterscheidbar. Alternative: zusätzlich ein Text (z. B. ein Fehlertext) oder ein Icon, das denselben Zustand
unabhängig von der Farbwahrnehmung kommuniziert.

</details>

## Responsive-Strategie

*(Fragen zu `howto_responsive-strategie.md`)*

<details>
<summary>Was ist der grundlegende Unterschied zwischen Progressive Enhancement und
Graceful Degradation?</summary>

Progressive Enhancement beginnt mit einer einfachen, garantiert funktionierenden Basis und erweitert sie,
sobald mehr Platz oder Möglichkeiten vorhanden sind. Graceful Degradation beginnt umgekehrt mit der vollen,
anspruchsvollen Version und lässt sie bei fehlenden Voraussetzungen kontrolliert zurückfallen.

</details>

<details>
<summary>Welche Media-Query-Richtung passt zu Mobile-First — <code>min-width</code>
oder <code>max-width</code> — und warum?</summary>

`min-width`: Die Basis-Regeln gelten für die kleinste Breite und werden ab einer bestimmten Breite nur
ergänzt, nie zurückgenommen — das entspricht der Erweiterungs-Richtung von Progressive Enhancement.

</details>

<details>
<summary>Ein Entwickler schreibt zuerst CSS für die volle Desktop-Breite und ergänzt
dann <code>max-width</code>-Regeln für kleine Bildschirme. Welcher Strategie entspricht das, und welches
Risiko birgt dieser Ansatz typischerweise?</summary>

Das ist strukturell Graceful Degradation (Desktop-First). Typisches Risiko: Der „Rückfall" für kleine
Bildschirme wird in der Praxis seltener gepflegt und getestet als die Version, mit der man begonnen hat.

</details>

<details>
<summary>Wie viele feste Breakpoints definiert Bootstrap standardmäßig, und was
unterscheidet sie technisch von eigenem CSS?</summary>

Fünf (`sm`, `md`, `lg`, `xl`, `xxl`). Technisch sind das nichts anderes als vordefinierte
`min-width`-Media-Queries, die über Klassen-Kürzel angesprochen werden, statt sie selbst zu schreiben.

</details>

<details>
<summary>Erklären Sie an einem eigenen, nicht aus der Fallstudie stammenden
Beispiel, wie eine einzige Klassenkombination zwei Bildschirmbreiten gleichzeitig beschreiben kann.</summary>

Offene Frage, Musterlösung z. B.: `col-12 col-md-6` beschreibt gleichzeitig „volle Breite unterhalb von
`md`" und „halbe Breite ab `md`" — eine einzige Klassenkombination für zwei Bildschirmbreiten, ganz ohne
eigene `@media`-Regel.

</details>

<details>
<summary>Welche Leitfrage sollten Sie sich laut Faustregel bei jeder
Layout-Entscheidung stellen?</summary>

„Was sieht die kleinste Breite? Was kommt ab welcher Breite dazu?" — nicht „Was fällt beim Verkleinern
weg?".

</details>

## Barrierefreiheit

*(Fragen zu `howto_barrierefreiheit.md`)*

<details>
<summary>Wofür steht das Akronym POUR?</summary>

Perceivable (wahrnehmbar), Operable (bedienbar), Understandable (verständlich), Robust (robust) — die vier
Grundprinzipien der WCAG.

</details>

<details>
<summary>Erklären Sie den grundsätzlichen Unterschied zwischen Usability und
Barrierefreiheit anhand der jeweiligen Zielgruppe.</summary>

Usability fragt, ob die *vorgesehene* Zielgruppe in einem bestimmten Nutzungskontext gut zurechtkommt.
Barrierefreiheit fragt, ob *irgendjemand*, der das Produkt nutzen möchte oder muss, ausgeschlossen wird —
ausdrücklich auch Personen außerhalb der ursprünglich geplanten Zielgruppe.

</details>

<details>
<summary>Seit wann ist Barrierefreiheit für öffentliche Stellen des Bundes in
Deutschland verbindlich vorgeschrieben?</summary>

Seit 2011 (Novelle 2019) durch die BITV 2.0, auf Basis des BGG von 2002.

</details>

<details>
<summary>Ist ein privates deutsches Unternehmen zur digitalen Barrierefreiheit
verpflichtet? Begründen Sie anhand der aktuellen Rechtslage.</summary>

Seit dem 28.06.2025 ja, für bestimmte Produkte/Dienstleistungen (u. a. Online-Shops, Bankdienstleistungen,
E-Books, Teile der Telekommunikation) — durch das Barrierefreiheitsstärkungsgesetz (BFSG), das die
EU-Richtlinie 2019/882 umsetzt. Davor war Barrierefreiheit für private Anbieter freiwillig; es gibt weiterhin
Ausnahmen, z. B. für Kleinstunternehmen bei reinen Dienstleistungen.

</details>

<details>
<summary>Auf welche gemeinsame technische Grundlage verweisen sowohl die BITV 2.0
als auch das BFSG inhaltlich?</summary>

Die europäische Norm EN 301 549, die ihrerseits weitgehend die internationalen WCAG übernimmt (meist
Konformitätsstufe AA).

</details>

<details>
<summary>Nennen Sie für jedes der vier POUR-Prinzipien eine konkrete, kleine
Umsetzungsmaßnahme (nicht aus der Fallstudie).</summary>

Offene Frage, Musterlösung z. B.: Wahrnehmbar — Alternativtext für Bilder; Bedienbar — vollständige
Tastaturbedienbarkeit mit sichtbarem Fokus; Verständlich — konkrete statt generische Fehlermeldungen;
Robust — valides, semantisches HTML, ARIA nur ergänzend.

</details>

<details>
<summary>Was besagt die Faustregel zum Verhältnis von nativem HTML und ARIA?</summary>

Ein natives HTML-Element mit passendem Attribut (z. B. `disabled`, `required`) ist oft schon barrierefrei —
ARIA ergänzt nur dort, wo sonst Information verloren ginge, und ersetzt niemals semantisches HTML.

</details>

## Ausblick: Interaktive Variante

Wer zusätzlich sofortiges Feedback, zufällige Reihenfolge oder eine einfache Zählung richtiger Antworten
möchte — vor allem sinnvoll für Fragen mit einer eindeutig richtigen Antwort —, kann diese Fragen später in
eine eigenständige HTML/JS-Quizseite überführen: eine einzelne Datei mit dem Fragenkatalog als
Datenstruktur, ohne Server oder Account, z. B. als einfache Multiple-Choice-Auswahl mit Sofort-Feedback. Für
Fragen mit offener Begründung bleibt auch dort der Abgleich mit einer Musterlösung die praktikable Form —
Automatisierung hilft hier wenig. Diese Datei (`kontrollfragen.md`) bleibt in jedem Fall die Quelle der
Wahrheit, aus der sich ein solcher Fragenkatalog bei Bedarf ableiten ließe.
