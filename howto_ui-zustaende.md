**UI-Zustände planen — Cheat-Sheet · Web-UI-Prototyping · LS10.2**

> Ausgangspunkt für Ihre Feinzustände (Arbeitsauftrag 1): drei Fragen an jedes Element, mit Beispielen aus
> der Fallstudie (`fallstudie/prototyp/`).

## Die drei Fragen

Jedes UI-Element kann aus bis zu drei ganz unterschiedlichen Gründen seinen Zustand ändern. Diese drei
Gründe sind voneinander unabhängig — ein Button kann zum Beispiel gleichzeitig deaktiviert **und** gerade
dabei sein zu laden. Stellen Sie sich deshalb für jedes Element Ihres Screens (Button, Textfeld, Liste …)
nacheinander die folgenden drei Fragen. Jede „Ja"-Antwort liefert Ihnen mögliche Zustände, die Sie als **Notiz** an dem
Zustand in Ihrem Diagramm festhalten, in dem sie auftreten.

### 1. Reagiert es auf Interaktion? → Interaktions-Zustände

`default → hover → focus → active → disabled`

Diese Zustände entstehen dadurch, dass eine Nutzer\*in unmittelbar mit dem Element interagiert —
unabhängig davon, was die Anwendung im Hintergrund tut oder ob eine Eingabe gültig ist. Ein Button
durchläuft typischerweise: Ruhezustand (`default`), Überfahren mit der Maus (`hover`), Erreichen per
Tastatur (`focus`), Betätigung (`active`) und, wenn er nicht bedienbar sein soll, `disabled`. Jeder dieser
Zustände lässt sich über eine CSS-Pseudoklasse (`:hover`, `:focus`, `:active`) oder ein HTML-Attribut
(`disabled`) ansprechen — Sie benötigen dafür kein JavaScript.

> **Beispiel (Fallstudie):** Der Button *Signieren* zeigt den deaktivierten Zustand: Nachdem ein Nachweis
> signiert wurde, verhindert das Attribut `disabled` eine zweite Signatur. Damit das nicht nur wie ein
> ausgegrauter Button wirkt, steht der Grund zusätzlich als Fließtext direkt daneben
> (`zustaende/signiert.html`) — mehr dazu im Abschnitt ARIA weiter unten.

### 2. Hängt es von Daten oder einem Vorgang ab? → Daten-/Prozess-Zustände

`leer → lädt → gefüllt/Erfolg → Fehler`

Diese Zustände hängen nicht von einer direkten Nutzerhandlung ab, sondern davon, in welcher Phase sich ein
Vorgang der Anwendung gerade befindet — meist beim Laden von Daten oder nach dem Absenden eines Formulars.
Typisch ist die Abfolge: Es gibt (noch) keine Daten (`leer`), die Daten werden gerade angefragt (`lädt`),
die Anfrage war erfolgreich (`gefüllt`/`Erfolg`) oder sie ist fehlgeschlagen (`Fehler`). Anders als bei den
Interaktions-Zuständen entscheidet hier die **App**, nicht die Nutzer\*in — deshalb tauchen diese Zustände
in Ihrem Diagramm oft als eigener Zustand auf, nicht nur als Notiz, bis hin zum zusammengesetzten Zustand
mit `entry`/`do` (siehe Vertiefung).

> **Beispiel (Fallstudie):** Die leere Liste erklärt, warum nichts zu sehen ist, und bietet einen sinnvollen
> nächsten Schritt an (`zustaende/uebersicht-leer.html`). Der Ladezustand zeigt Platzhalter-Balken
> (Skeleton) anstelle echter Inhalte (`zustaende/uebersicht-laden.html`, nur in der ausführlichen Fassung V4).

### 3. Nimmt es Eingaben entgegen, die geprüft werden? → Validierungs-Zustände

`unberührt → in Bearbeitung → gültig → ungültig`

Diese Zustände betreffen ausschließlich Eingabeelemente wie Textfelder oder Auswahllisten und beschreiben,
ob die aktuelle Eingabe den fachlichen Anforderungen entspricht. Ein Feld beginnt unberührt, wird während
der Eingabe bearbeitet und ist danach entweder gültig oder ungültig — mit einem erläuternden Fehlertext.
Bootstrap bildet das über die statischen Klassen `.is-valid`/`.is-invalid` ab; derselbe Zustand lässt sich
alternativ über die dynamischen CSS-Pseudoklassen `:valid`/`:invalid` erreichen, die der Browser automatisch
anhand von Validierungsattributen wie `required` setzt.

> **Beispiel (Fallstudie):** Das Kommentarfeld im Formular *Zurückweisungsgrund* zeigt den ungültigen
> Zustand: roter Rahmen plus ein Fehlertext, der erklärt, was fehlt (`zustaende/zurueckweisen.html`). Beide
> Umsetzungswege — statisch über `.is-invalid` und dynamisch über `:invalid` — stehen dort als Kommentar
> gegenübergestellt.

## Wer braucht welche Achse? (Ausgangspunkt für die eigene Planung)

| Element | Interaktions-Zustände | Daten-/Prozess-Zustände | Validierungs-Zustände |
|---|---|---|---|
| Button | Praktisch immer: sichtbare Reaktion auf Hover, Fokus und Klick nötig. | Häufig bei Submit-Buttons: deaktiviert + Ladehinweis während des Absendens. | Nur mittelbar, als Folge eines ungültigen Formulars. |
| Textfeld | Immer relevant, vor allem sichtbarer Fokus für Tastaturnutzer\*innen. | Selten, außer bei serverseitig vorausgefüllten Werten. | Zentral: gültig/ungültig/Pflichtfeld gehören genau hierher. |
| Liste/Übersicht | Teilweise: einzelne Zeilen reagieren auf Hover/Fokus. | Immer: leer, lädt und Fehler sind hier die typischen Zustände. | Nicht relevant — eine Liste nimmt keine zu prüfende Eingabe entgegen. |

Drei bis vier unterschiedliche Zustände (Niveau *Erweitert*, Kriterium 1/5) entstehen in der Praxis fast
immer dadurch, dass Sie Zustände aus **zwei verschiedenen Achsen** kombinieren — zum Beispiel einen
Interaktions-Zustand (`disabled`) und einen Daten-Zustand (`lädt`) am selben Button — statt vier Varianten
derselben Achse aneinanderzureihen.

## ARIA: Zustand auch hörbar machen

CSS macht einen Zustand **sichtbar** — eine rote Umrandung, ein ausgegrauter Button, ein Spinner. Wer die
Seite nicht sieht, sondern mit einem Screenreader hört (z. B. NVDA, JAWS, VoiceOver), braucht denselben
Zustand als gesprochene Information. Dafür gibt es ARIA (*Accessible Rich Internet Applications*): einen
offiziellen W3C-Standard, der denselben drei Achsen oben ein Vokabular gibt, das Browser und Screenreader
verstehen — kein viertes, eigenes Konzept, sondern dieselben Zustände in einer vorlesbaren Form.

**Wie liest ein Screenreader vor?** Für jedes fokussierte Element nennt er im Kern vier Dinge: den **Namen**
(meist der sichtbare Text oder das `<label>`), die **Rolle** (z. B. „Button", „Textfeld"), den **Zustand**
(z. B. „deaktiviert", „ungültig") und optional eine **Beschreibung** — zusätzlicher Text, der über
`aria-describedby` verknüpft ist und direkt nach dem Namen vorgelesen wird. Wer das Kommentarfeld unserer
Fallstudie per Tastatur erreicht, hört sinngemäß: „Grund der Zurückweisung, Eingabefeld, ungültig, bitte
geben Sie einen Grund an" — Name, Rolle, Zustand und Beschreibung in einem Satz.

Zwei Attribute verhalten sich dabei anders als die übrigen: `role="status"` erzeugt eine sogenannte
**Live-Region**. Ihr Inhalt wird automatisch vorgelesen, sobald er erscheint oder sich ändert — unabhängig
davon, wo sich der Fokus gerade befindet. Das ist bei der Lademeldung „Nachweise werden geladen …" wichtig:
Niemand muss aktiv dorthin navigieren, um zu erfahren, dass gerade geladen wird. `aria-hidden="true"` wirkt
umgekehrt: Es entfernt ein Element vollständig aus dem, was vorgelesen wird — sinnvoll für die
Platzhalter-Balken des Skeletons, die rein optisch sind und sonst als bedeutungslose Wiederholung vorgelesen
würden.

Eine weitere Besonderheit betrifft `disabled`: Ein nativ deaktivierter Button wird aus der Tab-Reihenfolge
entfernt — wer mit Tab navigiert, landet dort gar nicht erst. Genau deshalb muss die Erklärung, warum der
Button deaktiviert ist, an einer Stelle stehen, die weiterhin erreichbar bleibt — in unserer Fallstudie der
Text neben dem Button, verknüpft über `aria-describedby`.

| Zustand (Datei) | ARIA/HTML | Was vorgelesen wird |
|---|---|---|
| deaktiviert (`signiert.html`) | natives `disabled`; Grund per `aria-describedby` | Rolle „Button", Zustand „deaktiviert" — per Tab nicht erreichbar, der Text daneben schon. |
| ungültig (`zurueckweisen.html`) | `aria-invalid="true"` + `aria-describedby` | Zustand „ungültig", danach der Fehlertext als Beschreibung. |
| lädt (`uebersicht-laden.html`) | `role="status"`; `aria-hidden="true"` auf Platzhaltern | Wird automatisch vorgelesen, ohne dass dorthin navigiert werden muss. |
| ausgewählt/aktiv (`index.html`) | `aria-current="true"` | Zusätzlich wird „aktuell" angekündigt. |

> **Faustregel:** Ein natives HTML-Element mit passendem Attribut (`disabled`, `required`) ist oft schon
> barrierefrei — ARIA ergänzt nur, wo sonst Information verloren ginge (der *Grund*, ein laufender
> *Vorgang*). ARIA ersetzt niemals semantisches HTML, es ergänzt es.

> **Tellerrand:** `aria-describedby` verknüpft ein Element mit dem Text, der *erklärt, warum* — Farbe oder
> ein deaktivierter Button allein sagen das nicht. Derselbe Gedanke wie „Status als Text im Badge, nicht nur
> als Farbe" (Kriterium 7, Norm & Barrierefreiheit).

## Für Ihre Doku

- Welche der drei Fragen trifft auf Ihr Element zu? Halten Sie das Ergebnis als Notiz am betroffenen Zustand
  in Ihrem Diagramm fest.
- **Grundniveau:** mindestens zwei unterschiedliche Zustände. **Erweitert:** drei bis vier — am besten aus
  zwei verschiedenen Achsen statt vier Varianten derselben.
- Setzen Sie in Stufe 2 zuerst das native HTML-Attribut um und ergänzen Sie ARIA nur dort, wo es tatsächlich
  etwas Zusätzliches hörbar macht.
