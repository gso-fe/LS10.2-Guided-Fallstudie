**UI-Zustände planen — Cheat-Sheet · Web-UI-Prototyping · LS10.2**

> Ausgangspunkt für Ihre Feinzustände (Arbeitsauftrag 1): für jedes Element dieselben drei Auslöser prüfen,
> mit Beispielen aus der Fallstudie (`fallstudie/prototyp/`).

## Drei Auslöser für einen Zustandswechsel

Eine Oberfläche ist nie nur ein einziges, starres Bild: Praktisch jedes Element — ein Button, ein Textfeld,
eine ganze Liste — sieht je nachdem, was gerade passiert, anders aus oder verhält sich anders. Damit Sie
diese Vielzahl möglicher Zustände nicht an jedem Element neu erfinden müssen, lohnt sich ein systematischer
Blick auf die **Ursache**: Wodurch genau ändert sich der Zustand gerade?

Dafür genügen in aller Regel drei Auslöser, die unabhängig voneinander wirken — ein Element kann durchaus
von mehreren gleichzeitig betroffen sein. Ein alltägliches Beispiel: Ein Button zum Absenden eines Formulars
wird, sobald er geklickt wird, zugleich deaktiviert (damit niemand ein zweites Mal klickt) **und** zeigt
einen Ladehinweis wie einen Spinner oder den Text „Wird gesendet …", bis die Antwort vom Server eintrifft —
zwei unabhängige Auslöser an ein und demselben Element. Prüfen Sie deshalb für jedes Element Ihres Screens
(Button, Textfeld, Liste …) nacheinander, ob einer der folgenden drei Auslöser zutrifft. Jedes Zutreffen
liefert Ihnen mögliche Zustände, die Sie als **Notiz** an der betroffenen Stelle in Ihrem Diagramm festhalten.

### 1. Reagiert es auf Interaktion? → Interaktions-Zustände

`default → hover → focus → active → disabled`

Diese Zustände entstehen dadurch, dass eine Nutzer\*in unmittelbar mit dem Element interagiert —
unabhängig davon, was die Anwendung im Hintergrund tut oder ob eine Eingabe gültig ist. Ausgangspunkt ist
dabei immer **`default`**: der Ruhezustand, in dem sich das Element befindet, wenn die Seite fertig geladen
ist und noch niemand damit interagiert hat. Alle übrigen Interaktions-Zustände sind nichts weiter als eine
vorübergehende Abweichung von genau diesem Ruhezustand — sobald die Interaktion endet (die Maus wegbewegt,
der Fokus verlassen wird), kehrt das Element automatisch zu `default` zurück. Ein Button durchläuft
typischerweise: `default`, Überfahren mit der Maus (`hover`), Erreichen per Tastatur (`focus`), Betätigung
(`active`) und, wenn er nicht bedienbar sein soll, `disabled`. Dieselbe Abfolge betrifft nicht nur Buttons,
sondern jedes interaktive Element — Links, Formularfelder, Checkboxen. Jeder dieser Zustände lässt sich über
eine CSS-Pseudoklasse (`:hover`, `:focus`, `:active`) oder ein HTML-Attribut (`disabled`) ansprechen — Sie
benötigen dafür kein JavaScript.

> **Sonderfall `default`:** Anders als `hover`, `focus` oder `disabled` besitzt der Ruhezustand keine eigene
> CSS-„Auszeichnung" — der Begriff passt hier eigentlich nicht, weil es dafür weder eine Pseudoklasse noch ein
> Attribut gibt, das ihn markiert. „Leer" ist er trotzdem nicht: `default` ist einfach die normale,
> unqualifizierte Grundregel des Elements (z. B. `.btn { … }`) — alles, was Sie ohne Pseudoklasse oder
> Attribut-Selektor schreiben, gilt automatisch, solange keine spezifischere Regel (`:hover`, `:focus`,
> `[disabled]` …) gerade zutrifft. Zurückkehren müssen Sie dorthin auch nicht aktiv auslösen: Der Browser
> prüft die Selektoren laufend neu, und sobald z. B. die Maus das Element verlässt, greift `:hover` einfach
> nicht mehr — die Grundregel gilt dann automatisch wieder. Verwechslungsgefahr: CSS kennt zwar eine
> Pseudoklasse namens `:default`, die meint damit aber etwas völlig anderes — die ursprünglich vorausgewählte
> Option einer Gruppe (z. B. den anfangs markierten Radio-Button), nicht den hier gemeinten Ruhezustand.

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
mit `entry`/`do` (siehe Vertiefung). Dieselbe Abfolge begegnet Ihnen praktisch überall im Web: ein ladender
Newsfeed, eine Produktsuche mit Ergebnisliste oder eben der schon erwähnte Absenden-Button.

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
anhand von Validierungsattributen wie `required` setzt. Typische Beispiele sind eine E-Mail-Adresse ohne
„@", ein zu kurzes Passwort oder ein leer gebliebenes Pflichtfeld.

> **Beispiel (Fallstudie):** Das Kommentarfeld im Formular *Zurückweisungsgrund* zeigt den ungültigen
> Zustand: roter Rahmen plus ein Fehlertext, der erklärt, was fehlt (`zustaende/zurueckweisen.html`). Beide
> Umsetzungswege — statisch über `.is-invalid` und dynamisch über `:invalid` — stehen dort als Kommentar
> gegenübergestellt.

## Welcher Auslöser betrifft welches Element? (Ausgangspunkt für die eigene Planung)

| Element | Interaktions-Zustände | Daten-/Prozess-Zustände | Validierungs-Zustände |
|---|---|---|---|
| Button | Praktisch immer: sichtbare Reaktion auf Hover, Fokus und Klick nötig. | Häufig bei Submit-Buttons: deaktiviert + Ladehinweis während des Absendens. | Nur mittelbar, als Folge eines ungültigen Formulars. |
| Textfeld | Immer relevant, vor allem sichtbarer Fokus für Tastaturnutzer\*innen. | Selten, außer bei serverseitig vorausgefüllten Werten. | Zentral: gültig/ungültig/Pflichtfeld gehören genau hierher. |
| Liste/Übersicht | Teilweise: einzelne Zeilen reagieren auf Hover/Fokus. | Immer: leer, lädt und Fehler sind hier die typischen Zustände. | Nicht relevant — eine Liste nimmt keine zu prüfende Eingabe entgegen. |

Drei bis vier unterschiedliche Zustände (Niveau *Erweitert*, Kriterium 1/5) entstehen in der Praxis fast
immer dadurch, dass Sie Zustände aus **zwei verschiedenen Auslösern** kombinieren — wie im Beispiel oben:
ein Absenden-Button, der während des Sendens zugleich deaktiviert ist (Interaktions-Auslöser) und einen
Ladehinweis zeigt (Daten-/Prozess-Auslöser) — statt vier Varianten desselben Auslösers aneinanderzureihen.

## Zustand sichtbar machen: typisches CSS-Repertoire

Zustände werden fast immer über eine Kombination aus wenigen, immer wiederkehrenden CSS-Effekten sichtbar
gemacht — nicht über beliebig unterschiedliches Styling für jeden einzelnen Zustand. Nutzer\*innen nehmen
einen Zustandswechsel über drei Kanäle wahr, oft gleichzeitig:

- **Farbe/Deckkraft:** Hintergrund- oder Textfarbe ändert sich (`:hover` meist dezent dunkler/heller,
  `.is-invalid` rot, `.is-valid` grün), ein deaktiviertes Element wirkt blasser (`opacity`) und der
  Mauszeiger wechselt zu `cursor: not-allowed`.
- **Form/Bewegung:** ein Rahmen oder Schatten erscheint (`outline`/`box-shadow` bei `:focus-visible`, der
  rote Rahmen bei `:invalid`), oder etwas bewegt sich (ein rotierender Spinner beim Laden, ein kurzer
  Übergang via `transition` beim Hover, das Schimmern eines Skeleton-Platzhalters).
- **Text/Icon-Inhalt:** die eigentliche Beschriftung ändert sich (ein Button zeigt „Wird gesendet …" statt
  „Absenden", ein Badge wechselt von „eingereicht" zu „signiert") oder ein Icon kommt hinzu (ein Haken bei
  gültiger Eingabe, ein Ausrufezeichen bei ungültiger).

Wichtig für Barrierefreiheit (siehe auch den Tellerrand-Hinweis weiter unten): Farbe allein genügt nicht —
ein rein rot gerahmtes Feld ist für farbenblinde Nutzer\*innen kaum von einem gültigen zu unterscheiden.
Guter Zustands-Code kombiniert deshalb praktisch immer mindestens zwei dieser Kanäle, z. B. Farbe **und**
Text (roter Rahmen **und** Fehlertext), nicht Farbe allein.

## ARIA: Zustand auch hörbar machen

*(Wie sich Barrierefreiheit fachlich und rechtlich einordnet — Abgrenzung zu Usability/UX, Rechtslage in
Deutschland, die vier WCAG-Prinzipien POUR —, steht in `howto_barrierefreiheit.md`; hier geht es nur um die
konkrete ARIA-Umsetzung.)*

CSS macht einen Zustand wie oben beschrieben **sichtbar**. Wer die Seite nicht sieht, sondern mit einem
Screenreader hört (z. B. NVDA, JAWS, VoiceOver), braucht denselben Zustand als gesprochene Information.
Dafür gibt es ARIA (*Accessible Rich Internet Applications*): einen offiziellen W3C-Standard, der denselben
drei Auslösern oben ein Vokabular gibt, das Browser und Screenreader
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

- Welcher der drei Auslöser trifft auf Ihr Element zu? Halten Sie das Ergebnis als Notiz am betroffenen
  Zustand in Ihrem Diagramm fest.
- **Grundniveau:** mindestens zwei unterschiedliche Zustände. **Erweitert:** drei bis vier — am besten aus
  zwei verschiedenen Auslösern statt vier Varianten desselben Auslösers.
- Setzen Sie in Stufe 2 zuerst das native HTML-Attribut um und ergänzen Sie ARIA nur dort, wo es tatsächlich
  etwas Zusätzliches hörbar macht.
