**Responsive-Strategie — Progressive Enhancement vs. Graceful Degradation · Web-UI-Prototyping · LS10.2**

> Hintergrund zu Ihrem Responsive-Konzept (Dokumentationsvorlage § 2.3/§ 3.1, Arbeitsauftrag 2): warum
> Mobile-First keine Geschmacksfrage ist, sondern einer von zwei grundsätzlichen Wegen zu einer
> Oberfläche, die auf jedem Bildschirm funktioniert — und wie Media Queries, Breakpoints und das
> Grid-System diesen Weg technisch umsetzen.

## Zwei Strategien, ein Ziel

Jede Oberfläche muss auf unterschiedlichen Bildschirmgrößen funktionieren — vom Smartphone bis zum
großen Desktop-Monitor. Dafür gibt es zwei grundsätzlich entgegengesetzte Denkrichtungen.

**Progressive Enhancement** beginnt mit einer einfachen, schmalen Basis, die garantiert überall
funktioniert — eine Spalte, lesbarer Text, bedienbare Buttons, ohne besondere Voraussetzungen. Erst
danach wird diese Basis **erweitert**, sobald mehr Platz oder mehr Möglichkeiten vorhanden sind:
mehr Spalten, zusätzliche Inhalte, aufwendigere Interaktion. Die Grundversion ist nie kaputt — sie ist
nur einfacher.

**Graceful Degradation** geht den umgekehrten Weg: Zuerst entsteht die volle, anspruchsvolle
Erfahrung für moderne, große Bildschirme. Fehlen Voraussetzungen (wenig Platz, ältere Technik), soll
die Oberfläche **kontrolliert zurückfallen**, statt komplett zu versagen — im besten Fall „graceful",
also ohne dass etwas offensichtlich kaputt wirkt.

> **Beispiel (Fallstudie):** Die Fallstudie wählt konsequent Progressive Enhancement: `index.html`
> zeigt mobil zunächst nur die Liste (eine Spalte) — funktioniert vollständig, nichts fehlt für die
> Kernaufgabe. Erst ab der Bildschirmbreite `lg` kommt die Detailspalte **dazu**
> (`d-none d-lg-block`). Es gibt keine separate „Desktop-Vollversion", von der mobil etwas wegfällt.

| Aspekt | Progressive Enhancement | Graceful Degradation |
|---|---|---|
| Startpunkt | einfache, garantiert nutzbare Basis | volle, anspruchsvolle Version |
| Richtung | Bottom-up: Basis → Erweiterung | Top-down: Vollversion → Rückfall |
| Für alle nutzbar | ja, von Anfang an | nur die Vollversion ist optimiert |
| Typisches Risiko | Erweiterung wird vergessen | Rückfall wird nie getestet |
| In dieser LS | **Leitprinzip** (Mobile-First, wenig JS) | nicht verwendet |

Beide Strategien verfolgen dasselbe Ziel — eine Oberfläche, die robust auf unterschiedlichen
Voraussetzungen funktioniert —, unterscheiden sich aber genau darin, **wo das Risiko liegt**: Bei
Progressive Enhancement ist die Basis das Sichere, die Erweiterung das Zusätzliche. Bei Graceful
Degradation ist die Vollversion das Ziel, der Rückfall die Notlösung — und Notlösungen werden in der
Praxis seltener gepflegt und getestet als das, womit man beginnt.

## Mobile-First ist angewandte Progressive Enhancement

**Mobile-First** heißt: Sie schreiben CSS zuerst **für die kleinste Bildschirmbreite**, ohne
Media Query. Diese Basis-Regeln gelten **immer** — auch auf dem größten Monitor, sofern nichts
Spezifischeres sie überschreibt. Erst danach fügen Sie `min-width`-Media-Queries hinzu, die ab einer
bestimmten Breite **zusätzliche** Regeln ergänzen. Nichts wird weggenommen, nur ergänzt — genau das
Prinzip von Progressive Enhancement, nur auf CSS angewendet.

Der Gegenentwurf wäre **Desktop-First**: Basis-Regeln für die volle Breite, danach
`max-width`-Media-Queries, die ab einer bestimmten Breite Regeln **zurücknehmen** oder überschreiben.
Das ist strukturell Graceful Degradation — und einer der Gründe, warum Mobile-First heute der
Standardweg ist: Sie bauen nie etwas, das Sie später wieder abbauen müssen.

## Technische Grundlagen

### Media Queries

Eine Media Query ist eine CSS-Bedingung, die Regeln nur unter bestimmten Bedingungen gelten lässt —
am häufigsten abhängig von der Bildschirmbreite:

```css
@media (min-width: 992px) {
  .detail-pane { display: block; }
}
```

Mobile-First bedeutet konkret: Sie verwenden fast ausschließlich `min-width` (= „ab dieser Breite
**zusätzlich**"), nicht `max-width` (= „bis zu dieser Breite **noch**"). `min-width` passt zur
Erweiterungs-Richtung von Progressive Enhancement; `max-width` zur Rückfall-Richtung von Graceful
Degradation.

### Breakpoints

Ein Breakpoint ist die konkrete Bildschirmbreite, ab der eine Media Query greift. Bootstrap definiert
fünf feste Breakpoints — das sind einfach benannte, vordefinierte `min-width`-Werte, die Sie über
Klassen-Kürzel ansprechen, ohne selbst eine Media Query zu schreiben:

| Kürzel | ab Breite (`min-width`) | Typisches Gerät |
|---|---|---|
| *(kein Kürzel)* | 0 px — gilt immer | Smartphone, hochkant |
| `sm` | 576 px | Smartphone, quer |
| `md` | 768 px | Tablet |
| `lg` | 992 px | Tablet quer / kleiner Desktop |
| `xl` | 1200 px | Desktop |
| `xxl` | 1400 px | großer Desktop |

Die Klassen ohne Kürzel (z. B. `col-12`) sind Ihre Progressive-Enhancement-Basis — sie gelten ab
0 px und damit für **jede** Breite, sofern keine präfigierte Klasse sie für größere Breiten
überschreibt.

### Grid-Systeme

Ein Grid-System teilt die verfügbare Breite in ein festes Raster — bei Bootstrap **zwölf Spalten** je
Zeile (`row`). `col-6` belegt 6 von 12 Spalten (die Hälfte), unabhängig von der Bildschirmbreite.
Kombiniert mit Breakpoint-Kürzeln entsteht die eigentliche Stärke: `col-12 col-lg-5` heißt „volle
Breite, ab `lg` nur noch 5 von 12 Spalten" — eine einzige Klassenkombination beschreibt **beide**
Breiten gleichzeitig, ganz ohne eigene Media Query.

## Bootstrap in der Praxis

> **Beispiel (Fallstudie, `index.html`):** Die Liste trägt die Klassen `col-12 col-lg-5`: mobil
> (kein Breakpoint erreicht) volle Breite, ab `lg` nur noch 5 von 12 Spalten — Platz für die
> Detailspalte daneben. Diese trägt `col-12 col-lg-7 d-none d-lg-block`: `d-none` blendet sie
> standardmäßig aus (Basis: nicht vorhanden), `d-lg-block` **schaltet sie ab `lg` wieder ein** — die
> Erweiterung kommt **hinzu**, die mobile Basis bleibt unangetastet.

Was `d-lg-block` im Hintergrund tut, ist nichts anderes als die Media Query von oben, fertig
verpackt in eine Klasse:

```css
/* vereinfacht, sinngemäß das, was d-lg-block bewirkt */
@media (min-width: 992px) {
  .d-lg-block { display: block; }
}
```

Bootstraps Utility- und Grid-Klassen sind also kein eigenes Konzept — sie sind Media Queries und
Breakpoints, nur als wiederverwendbare Klassen statt als eigenes CSS geschrieben. Wer die Klassen
nutzt, wendet Progressive Enhancement an, ohne eine einzige Media Query selbst zu formulieren.

> **Faustregel:** Fragen Sie bei jeder Layout-Entscheidung: „Was sieht die kleinste Breite? Was kommt
> ab welcher Breite **dazu**?" — nicht „Was fällt beim Verkleinern weg?". Die erste Frage ist
> Progressive Enhancement, die zweite Graceful Degradation.

## Für Ihre Doku

- Benennen Sie in Ihrem Responsive-Konzept (§ 2.3) **ausdrücklich**, was Ihre mobile Basis ist und was
  der Desktop **zusätzlich** bekommt — nicht nur, dass „es auf dem Desktop anders aussieht".
- Prüfen Sie in der Umsetzung (§ 3.1): Haben Sie mit `min-width`-Denken gearbeitet (Bootstrap-Klassen
  ohne Präfix als Basis, Präfixe als Erweiterung) oder sind Ihnen `max-width`-Regeln hineingerutscht?
- Ein Layoutwechsel mobil↔Desktop (einspaltig → mehrspaltig) ist im Grundniveau Pflicht — er ist
  automatisch Progressive Enhancement, wenn die mobile Fassung für sich allein vollständig nutzbar
  bleibt.
