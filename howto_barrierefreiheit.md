**Barrierefreiheit — Einordnung, Pflichten & POUR · Web-UI-Prototyping · LS10.2**

> Hintergrund zu Kriterium 7 (Norm & Barrierefreiheit): wie sich Barrierefreiheit von Usability, User
> Experience und allgemeiner Softwarequalität abgrenzt, was in Deutschland rechtlich gilt (BITV 2.0,
> Barrierefreiheitsstärkungsgesetz) und wie die internationalen WCAG-Prinzipien (POUR) sich in konkrete,
> kleine Maßnahmen übersetzen lassen. Die technische Umsetzung mit ARIA steht ausführlich in
> `howto_ui-zustaende.md`, Abschnitt „ARIA: Zustand auch hörbar machen" — dieses Dokument liefert die
> Einordnung davor.

## Einordnung: Barrierefreiheit zwischen Softwarequalität, Usability und UX

In der Praxis werden Barrierefreiheit, Usability und User Experience oft synonym verwendet — fachlich sind
es aber vier gestaffelte, in eigenen Normen definierte Begriffe:

| Begriff | Leitfrage | Bezugsnorm | Für wen |
|---|---|---|---|
| Softwarequalität | Funktioniert die Software korrekt, sicher, performant, wartbar? | DIN EN ISO/IEC 25010 | alle Stakeholder, auch Betrieb und Wartung |
| Usability (Gebrauchstauglichkeit) | Können definierte Nutzer\*innen definierte Ziele effektiv, effizient und zufriedenstellend erreichen? | ISO 9241-11 | die vorgesehene Zielgruppe, in einem bestimmten Nutzungskontext |
| User Experience (UX) | Wie fühlt sich die gesamte Erfahrung an — vor, während und nach der Nutzung? | ISO 9241-210 | dieselbe Zielgruppe, zusätzlich mit Emotion/Wahrnehmung |
| Barrierefreiheit (Accessibility) | Ist das Produkt auch für Menschen mit der größtmöglichen Bandbreite an Fähigkeiten nutzbar? | ISO 9241-171, WCAG | ausdrücklich **alle**, auch außerhalb der geplanten Zielgruppe |

Softwarequalität (ISO 25010) führt Benutzbarkeit als eines von acht gleichrangigen Merkmalen neben z. B.
Sicherheit oder Wartbarkeit. User Experience erweitert Usability um die emotionale, ganzheitliche Seite
derselben Zielgruppe. **Barrierefreiheit setzt eine andere Klammer:** Sie fragt nicht „ist es für die
Zielgruppe gut nutzbar", sondern „schließt die Umsetzung *irgendjemanden* aus, der es nutzen möchte oder
muss" — unabhängig davon, ob diese Person Teil der ursprünglich geplanten Zielgruppe war.

> **Faustregel:** Gute Usability/UX und Barrierefreiheit sind unabhängige Qualitätsdimensionen, auch wenn
> sie sich meist gegenseitig verstärken. Ein hübsches, aber nur per Maus bedienbares Drag-and-Drop-Interface
> kann exzellente UX für die geplante Zielgruppe **und** keine Barrierefreiheit zugleich haben. Umgekehrt
> kann eine Seite rein technisch alle WCAG-Kriterien erfüllen und trotzdem mühsam zu benutzen sein — Normen
> prüfen Konformität, nicht Gestaltungsqualität.

## Rechtslage in Deutschland: Pflicht oder Kür?

| Jahr | Regelung | Geltungsbereich |
|---|---|---|
| 2002 | BGG (Behindertengleichstellungsgesetz) | Grundsatznorm für öffentliche Stellen des Bundes |
| 2011, Novelle 2019 | BITV 2.0 (Barrierefreie-Informationstechnik-Verordnung) | konkretisiert das BGG für Websites/Apps öffentlicher Stellen des Bundes; setzt EU-Richtlinie 2016/2102 um |
| 2019 | EU-Richtlinie 2019/882 „European Accessibility Act" | EU-weite Vorgabe, nationale Umsetzung verpflichtend |
| seit 28.06.2025 | BFSG (Barrierefreiheitsstärkungsgesetz) | setzt die EU-Richtlinie in Deutschland um; erstmals verpflichtend für bestimmte **private** Produkte/Dienstleistungen |

Für **öffentliche Stellen** (Bundesbehörden, über Landesrecht meist auch Länder und Kommunen) ist
Barrierefreiheit schon seit über zehn Jahren verbindlich vorgeschrieben. Für **private Unternehmen** war sie
bis vor kurzem reine Kür — bis das BFSG am 28. Juni 2025 in Kraft trat. Es verpflichtet seitdem Anbieter
bestimmter Produkte und Dienstleistungen (u. a. Online-Shops, Bankdienstleistungen, E-Books, Teile der
Telekommunikation) zur Barrierefreiheit, mit Ausnahmen etwa für Kleinstunternehmen bei reinen
Dienstleistungen. Das beträfe potenziell auch eine reale Anwendung hinter dieser Fallstudie, falls ein
Ausbildungsbetrieb sie produktiv einsetzen würde.

Beide Gesetze definieren inhaltlich nicht neu, *was* barrierefrei bedeutet, sondern verweisen auf dieselbe
technische Grundlage: die europäische Norm **EN 301 549**, die ihrerseits weitgehend die internationalen
**WCAG** (*Web Content Accessibility Guidelines*) des W3C übernimmt — meist auf **Konformitätsstufe AA**.
WCAG ist damit kein deutsches oder europäisches, sondern ein weltweit anerkanntes, von einzelnen Gesetzen
unabhängiges Regelwerk, das beide Rechtsnormen nur zitieren. Aktuell gilt WCAG 2.1/2.2; eine grundlegend
überarbeitete Version 3.0 ist in Arbeit, aber noch nicht final.

## POUR: Von vier Prinzipien zu konkreten Maßnahmen

Die WCAG ordnen alle konkreten Prüfkriterien vier übergeordneten Prinzipien zu — dem Akronym **POUR**:
*Perceivable* (wahrnehmbar), *Operable* (bedienbar), *Understandable* (verständlich), *Robust* (robust).
Jedes Prinzip lässt sich an einem einzigen, einfachen Beispiel durchdeklinieren: einem gewöhnlichen
**Kontaktformular** mit einem Foto des Support-Teams, drei Eingabefeldern und einem Absenden-Button.

### P — Wahrnehmbar (*Perceivable*)

Inhalte müssen über mindestens einen Sinneskanal wahrnehmbar sein, der der Nutzer\*in gerade zur Verfügung
steht — nicht jede\*r sieht, hört oder unterscheidet Farben gleich gut.

- **Alternativtext für Bilder:** Das Team-Foto bekommt `alt="Vierköpfiges Support-Team im Büro"`, nicht nur
  einen Dateinamen (siehe `guided-fallstudie.md`, Abschnitt Bilder).
- **Ausreichender Farbkontrast:** Der Formulartext bleibt auch bei eingeschränktem Sehen oder auf einem
  hellen Außen-Display lesbar (WCAG AA fordert i. d. R. mindestens 4.5:1 für Fließtext).
- **Nicht nur Farbe:** Ein fehlerhaft ausgefülltes Feld wird nicht nur rot, sondern bekommt zusätzlich einen
  Fehlertext (siehe `howto_ui-zustaende.md`, Abschnitt „Zustand sichtbar machen").

### O — Bedienbar (*Operable*)

Alle Funktionen müssen auch ohne Maus erreichbar sein, in angemessener Zeit und ohne Inhalte, die z. B.
durch Blitzeffekte Anfälle auslösen könnten.

- **Tastatur-Bedienbarkeit:** Durch alle drei Felder und den Absenden-Button lässt sich allein mit
  Tab/Shift+Tab und Enter navigieren, ganz ohne Maus.
- **Sichtbarer Fokus:** Das aktuell fokussierte Feld bekommt einen deutlichen Rahmen (`:focus-visible`,
  siehe `guided-fallstudie.md`, Abschnitt State-Pseudoklassen).
- **Genug Zeit:** Eine eventuelle Sitzungs-Zeitbegrenzung beim Ausfüllen lässt sich verlängern, statt
  eingegebene Daten kommentarlos zu verwerfen.

### U — Verständlich (*Understandable*)

Inhalt, Bedienung und Fehlermeldungen müssen vorhersehbar und klar formuliert sein.

- **Sprache angeben:** `<html lang="de">` sorgt dafür, dass ein Screenreader das Formular korrekt auf
  Deutsch vorliest, nicht mit englischer Aussprache.
- **Konkrete Fehlermeldungen:** Statt nur „Fehler" steht da „Bitte geben Sie eine gültige E-Mail-Adresse
  ein" (siehe `howto_ui-zustaende.md`, Abschnitt Validierungs-Zustände).
- **Konsistente Beschriftung:** Der Absenden-Button heißt auf jeder Seite des Formulars gleich, nicht mal
  „Weiter", mal „Absenden", mal „OK".

### R — Robust

Der Inhalt muss von möglichst vielen, auch zukünftigen Technologien zuverlässig interpretierbar sein —
insbesondere von Hilfsmitteln wie Screenreadern.

- **Valides, semantisches HTML:** ein echtes `<label for="…">` statt nur optisch danebenstehendem Text
  (siehe `guided-fallstudie.md`, Abschnitt Label).
- **ARIA nur ergänzend:** Wo natives HTML nicht reicht (z. B. der *Grund* für einen deaktivierten Button),
  ergänzt `aria-describedby` das Nötigste — mehr dazu in `howto_ui-zustaende.md`, Abschnitt ARIA.
- **Name, Rolle, Zustand korrekt:** Jedes Element nennt einem Screenreader verlässlich, was es ist (Rolle),
  wie es heißt (Name) und in welchem Zustand es ist — nicht nur visuell erkennbar.

> **Beispiel (Fallstudie):** Auch ohne einen einzigen Produktions-Server zeigt der Klickdummy bereits
> mehrere POUR-Maßnahmen in der Praxis: Der sichtbare Fokus-Rahmen (`:focus-visible` in `css/styles.css`)
> ist *Bedienbarkeit*, die konkrete Fehlermeldung im Formular *Zurückweisungsgrund*
> (`zurueckweisen.html`) ist *Verständlichkeit*, und die Verknüpfung von Button und Begründung über
> `aria-describedby` (`signiert.html`) ist *Robustheit*. Die vollständige Zuordnung von ARIA-Attributen zu
> Dateien steht in `howto_ui-zustaende.md`, Abschnitt „ARIA: Zustand auch hörbar machen".

## Weiterführend: ARIA im Detail

Dieses Dokument ordnet Barrierefreiheit nur ein — die konkrete technische Umsetzung mit ARIA-Attributen
(`aria-describedby`, `aria-invalid`, `role="status"`, `aria-hidden`, `aria-current` …) und wie ein
Screenreader das vorliest, steht ausführlich in `howto_ui-zustaende.md`, Abschnitt „ARIA: Zustand auch
hörbar machen". Die dortige Faustregel gilt auch hier: natives HTML zuerst umsetzen, ARIA nur dort
ergänzen, wo sonst Information verloren ginge.

## Quellen & weiterführende Links

**Normen** (keine frei zugänglichen Volltexte, in Doku/Literatur reicht das Kurzzitat):
- DIN EN ISO/IEC 25010 — Softwarequalitätsmodell, acht Qualitätsmerkmale, u. a. Benutzbarkeit
- ISO 9241-11 — Definition von Usability (Effektivität, Effizienz, Zufriedenheit)
- ISO 9241-210 — Definition von User Experience
- ISO 9241-171 / EN 301 549 — Software- bzw. IKT-Zugänglichkeit; EN 301 549 ist die technische Brücke, auf
  die sowohl BITV 2.0 als auch das BFSG verweisen

**Gesetze (Deutschland)** — vereinfachte Darstellung für Unterrichtszwecke, keine Rechtsberatung:
- [BITV 2.0](https://www.gesetze-im-internet.de/bitv_2_0/) — verbindlich für Websites/Apps öffentlicher
  Stellen des Bundes
- [BGG](https://www.gesetze-im-internet.de/bgg/) — Grundsatznorm, auf der die BITV 2.0 aufbaut
- [BFSG](https://www.gesetze-im-internet.de/bfsg/) — seit 28.06.2025 verbindlich für bestimmte private
  Produkte/Dienstleistungen

**International:**
- [WCAG 2.2 (W3C)](https://www.w3.org/TR/WCAG22/) — die aktuelle Fassung der Richtlinien
- [WCAG 2.1 Quick Reference](https://www.w3.org/WAI/WCAG21/quickref/) — durchsuchbare, nach POUR gegliederte
  Kurzfassung aller Prüfkriterien

## Für Ihre Doku

- Nennen Sie in Ihrer Dokumentation (Kriterium 7), an welchem WCAG-Konformitätslevel Sie sich orientieren
  (üblicherweise **AA**) — „barrierefrei" ohne Bezugsgröße ist keine prüfbare Aussage.
- Gehen Sie Ihren eigenen Screen einmal gezielt mit den vier POUR-Fragen durch, statt Barrierefreiheit als
  einen einzelnen, abstrakten Punkt zu behandeln.
- Es reicht, **zwei bis drei konkrete Maßnahmen** zu benennen und kurz zu begründen (z. B. Fokus-Rahmen,
  Alternativtext, Fehlertext statt Farbe) — nicht alle vier Prinzipien lückenlos abzudecken.
- Prüfen Sie zuerst natives HTML (Kriterium 3/4); ARIA ergänzt nur die Lücken (siehe
  `howto_ui-zustaende.md`).
