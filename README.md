# Aufgeweckt. KI-Klartext zum Frühstück

Impuls von EDGE Digital beim **Netzwerkfrühstück der LTM im K64**, Lübeck,
**20. August 2026, ab 8:30 Uhr**. 24 Folien, etwa 40 Minuten plus offenes Q&A.
Referenten: Edgar Paul-Ghazaryan (Eddie) und Emre Erdogan.

## Live

**https://edgarpauledge.github.io/cbl-aufgeweckt/**
GitHub Pages aus `main`, Repo `EdgarPaulEDGE/cbl-aufgeweckt`, öffentlich.
Jeder Push auf `main` geht automatisch live, das dauert etwa eine Minute.
Die Karte zum Mitnehmen liegt unter `/karte.html`.

Der Termin ist keine Werbeveranstaltung. Eike-Christian Fock stellt EDGE seinem
eigenen Netzwerk vor, die Eigenwerbung läuft über Inhalt. Deshalb gibt es im
ganzen Deck **keine Leistungsübersicht, keinen Case und keinen Call-to-Action**.

## Bedienung

| Taste | Wirkung |
|---|---|
| Pfeil rechts / links | Blättern |
| **S** | Redneransicht mit allen Regie-Notizen |
| **F** | Vollbild |
| **O** | Übersicht über alle Folien |
| **Esc** | Zurück aus der Übersicht |

`?nofrag` an die Adresse hängen zeigt alle Einblendungen sofort. Praktisch für
die Durchsicht und für den PDF-Export.

## Lokal starten

```bash
npm run serve
```

Dann `http://localhost:8080` öffnen. Die Präsentation läuft vollständig ohne
Internet: reveal.js, die Schriften und die Galaxie liegen im Projekt.

```bash
npm run build
```

Das ist kein Kompilat, sondern eine Bauprüfung: sie liest `index.html`, sammelt
alle lokalen Verweise und meldet fehlende Dateien. Ein Bild, das nicht existiert,
fällt im Browser stumm aus und man merkt es sonst erst vor Publikum.

```bash
npm install     # einmalig, holt puppeteer
npm run pruefe        # misst jede Folie auf Überlauf, legt PNGs in .pruefung/
npm run pruefe-karte  # prüft, ob die Karte über die Papierkante läuft
```

`npm run pruefe` ist die wichtigere der beiden Prüfungen. Reveal schneidet zu
hohe Folien kommentarlos ab: kein Fehler, keine Scrollleiste, der Inhalt ist
einfach unsichtbar. Das Skript navigiert zu jeder Folie, misst jedes Element
gegen den Rand und meldet, was rausläuft. Beide Skripte brauchen einen
laufenden `npm run serve` in einem zweiten Fenster.

## Dateien

**Für den Vortrag**
- `index.html` — die Präsentation, läuft offline
- `REGIE.md` — Zeitplan, Rollenverteilung, Streichliste, Checkliste vor Ort
- `FRAGEN.md` — die absehbaren Fragen aus dem Publikum mit kurzen Antworten

**Für den Frühstückstisch**
- `karte.html` — Karte zum Mitnehmen, A5 quer, beidseitig. Vorderseite die
  acht Punkte, Rückseite die vier Bausteine und ein Prompt zum Abschreiben.
  Drucken über Chrome, A4, Ränder "keine", Hintergrundgrafiken einschalten.
  Zwei Karten passen auf ein A4-Blatt.

## Bilder

Zwei Bilder im Deck sind mit KI erzeugt (Higgsfield, GPT Image 2) und beide
gekennzeichnet:

- `assets/images/fruehstueck.jpg` auf der Trennfolie vor den drei Fällen
- `assets/images/tagungsraum-ki.jpg` auf der Folie zur Kennzeichnungspflicht

Das zweite ist Absicht bis ins Detail: es ist genau die Sorte Hochglanzbild, die
ein Haus auf Instagram stellt, es trägt die Kennzeichnung, die Artikel 50
verlangt, und hinter seinen Fenstern liegen Berge, die es an der Ostsee nicht
gibt. Damit belegt es beide Aussagen des Blocks auf einmal.

Wer die Bilder austauscht: die Kennzeichnung muss mit. Ein Deck, das die Pflicht
erklärt und selbst dagegen verstößt, verliert den Raum.

## Gestaltung

Übernommen aus der SoulByte-Schulung, damit alle EDGE-Auftritte gleich aussehen:
Raumschwarz `#030309`, Avenir Next, Galaxie-Hintergrund aus `kosmos.js`
(three.js in `vendor/`, 2D-Sternenfeld als Rückfall), Schlüsselwörter im
Farbverlauf Purple zu Blau zu Cyan.

Regeln, die im Deck gelten: keine Dashes, keine Emojis, kein Monospace, kein
`box-shadow` (bricht den PDF-Export über decktape). Folien scrollen nicht,
Überlauf wird kommentarlos abgeschnitten.

Logos: EDGE links oben, Convention Bureau Lübeck rechts oben. Auf Titel- und
Trennfolien (`data-chrome="aus"`) verschwinden beide samt Seitenzahl.

## Offene Punkte vor dem 20. August

1. **Beamer und WLAN im K64 bestätigen lassen** (Ansprechpartnerin: Julia
   Dreefs). Der Live-Teil in Block 3 ist der stärkste Abschnitt. Ohne Netz
   tragen die Folien 11 bis 13 allein, sie enthalten die vollständige
   Gegenüberstellung.
2. **Teilnehmerzahl.** Eike rechnet mit sechs bis zwölf Personen. Das Deck
   funktioniert sitzend am Frühstückstisch genauso wie vor zwanzig Leuten.
3. **Karte drucken**, so viele Exemplare wie Gedecke plus fünf.
4. **Live-Moment auf Folie 18 vorbereiten:** einmal selbst durchspielen, was die
   KI auf eine Lübsche Frage antwortet, die die Runde selbst prüfen kann.

Folie 19 erzählt die Open-Book-Klausur von 2023: ChatGPT 3.5 gefragt, nicht
gegengelesen, beide durchgefallen. Die Geschichte ist echt und steht bewusst
direkt hinter der Halluzinations-Folie, weil sie deren Aussage belegt: man
sieht es dem Text nicht an. Erst danach kommt mit der Kennzeichnungspflicht
der Sprung ins Recht.

## Abgrenzung zu den anderen beiden Terminen

Der 26.08. in Travemünde und der 09.09. im Atlantic richten sich an Kunden des
Convention Bureau, also an Veranstaltungsplanerinnen und Planer. Hier im K64
sitzen Partner und Dienstleister der Region: Locations, Hotels, Gastronomie.
Alle Beispiele in diesem Deck kommen deshalb aus deren Alltag und nicht aus dem
Planeralltag.
