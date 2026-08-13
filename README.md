# Aufgeweckt. KI-Klartext zum Frühstück

Impuls von EDGE Digital beim **Netzwerkfrühstück der LTM im K64**, Lübeck,
**20. August 2026, ab 8:30 Uhr**. 25 Folien, etwa 40 Minuten plus offenes Q&A.
Referenten: Edgar Paul-Ghazaryan (Eddie) und Emre Erdogan.

## Live

**https://aufgeweckt.edge-digital.ai/**
GitHub Pages aus `main`, Repo `EdgarPaulEDGE/cbl-aufgeweckt`, öffentlich.
Jeder Push auf `main` geht automatisch live, das dauert etwa eine Minute.
Die Karte zum Mitnehmen liegt unter `/karte.html`.

Die alte Adresse `edgarpauledge.github.io/cbl-aufgeweckt/` leitet dorthin um.

**Domain:** `CNAME` im Repo hält den Namen, der DNS-Eintrag liegt bei Wix
(die Nameserver von `edge-digital.ai` zeigen auf `ns8/ns9.wixdns.net`, nicht
auf den Registrar). Dort steht ein CNAME `aufgeweckt` auf
`edgarpauledge.github.io`, genau wie bei `visionista.edge-digital.ai`.
Reihenfolge beim nächsten Mal: erst den DNS-Eintrag setzen, dann die
`CNAME`-Datei ins Repo. Andersherum leitet GitHub sofort auf einen Namen um,
der noch nicht auflöst, und die Seite ist zwischenzeitlich tot.

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

## Ohne Adressleiste zeigen

Drei Wege, vom schnellsten zum saubersten:

**1. Taste F.** Sobald die Seite geladen ist, einmal `F` drücken. Das ist der
eingebaute Vollbildmodus von reveal.js und blendet Adressleiste, Tabs und Dock
komplett aus. Zurück mit `Esc`. Funktioniert in Chrome und Safari gleich.

**2. Als App installieren.** Chrome bietet über das Dreipunktmenü
*Streamen, Speichern und Teilen → Seite als App installieren* an, Safari über
*Ablage → Zum Dock hinzufügen*. Danach liegt der Vortrag als eigenes Symbol im
Dock und startet in einem Fenster ganz ohne Browserleisten. Möglich macht das
`manifest.webmanifest` mit `"display": "fullscreen"`.

**3. Doppelklick auf `Vollbild starten.command`.** Startet Chrome im
Kiosk-Modus direkt mit der Live-Adresse: kein Fensterrahmen, keine Leisten,
nichts. Beenden mit `cmd+Q`. Das ist der Weg für den Vortragstag, weil nichts
schiefgehen kann und niemand versehentlich eine Leiste einblendet.

Beim ersten Start fragt macOS bei der `.command`-Datei einmal nach, ob sie
ausgeführt werden darf.

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
npm install           # einmalig, holt puppeteer
npm run pruefe-alles  # die vier Layoutprüfungen nacheinander
npm run pruefe-karte  # prüft, ob die Karte über die Papierkante läuft
```

Alle Prüfskripte brauchen einen laufenden `npm run serve` in einem zweiten
Fenster. Sie fahren jede Folie an und messen im Browser, weil sich Layoutfehler
im Quelltext nicht sehen lassen:

| Skript | Findet |
|---|---|
| `pruefe-folien.mjs` | Inhalt außerhalb der Folie. Reveal schneidet zu hohe Folien kommentarlos ab, ohne Fehler und ohne Scrollleiste. Legt zusätzlich von jeder Folie ein PNG in `.pruefung/`. |
| `pruefe-ueberlappung.mjs` | Kästen, die sich gegenseitig überdecken. Passiert mitten auf der Folie, wo weder Rand- noch Kantenprüfung anschlägt. |
| `pruefe-ausrichtung.mjs` | Kanten, die um 1 bis 24 Pixel danebenliegen. Genau dieser Graubereich liest sich als Fehler, größere Abstände liest das Auge als Absicht. |
| `pruefe-verzerrung.mjs` | Bilder, die verzerrt dargestellt werden: das gezeigte Seitenverhältnis gegen das der Datei. Passiert lautlos, sobald ein Bild mit fester Höhe in einer Spalten-Flexbox landet, die es auf ihre Breite streckt. |
| `pruefe-bilder.mjs` | Vollbericht über jedes Bild: Dateimaße, dargestellte Größe, Beschnitt durch `object-fit: cover`, Auflösungsreserve. Kein Test, sondern die Tabelle zum Draufschauen. |
| `pruefe-reihenfolge.mjs` | Einblendungen, die gegen die Leserichtung springen, und Folien, deren Kopfzeile beim Blättern noch fehlt. |

Die vier decken unterschiedliche Fehlerklassen ab, deshalb ersetzt keines das
andere. Die Überlappungsprüfung kam dazu, nachdem sich auf der Halluzinations-
Folie zwei Kästen 54 Pixel weit überdeckt hatten und die beiden älteren
Prüfungen das nicht sahen.

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

Alle Bilder im Deck sind mit KI erzeugt (Higgsfield) und gekennzeichnet:

- `assets/images/fruehstueck.jpg` und `schreibtisch.jpg` auf den beiden
  Trennfolien, `tagungsraum-ki.jpg` auf der Folie zur Kennzeichnungspflicht
  (GPT Image 2)
- `assets/images/robo/` der Begleiter: drei Freisteller mit Transparenz
  (`winkt`, `daumen`, `ratlos`) und vier Ortsbilder (`holstentor`, `passat`,
  `strandkorb`, `muk`), alle mit Nano Banana 2 aus drei Vorlagen gebaut, die
  auf dem Schreibtisch lagen: ein Roboter-Render, eine Mütze mit der
  Stickerei "ich ❤️ fischbrötchen" und ein Fischbrötchen. Die Orte kannte das
  Modell von selbst, Referenzfotos waren nicht nötig. Freigestellt wurde über
  den Background-Remover, nicht über eine Weiß-Maske: die Kanten an Fingern
  und Antennen halten das sonst nicht aus.

Der Tagungsraum ist Absicht bis ins Detail: es ist genau die Sorte Hochglanzbild,
die ein Haus auf Instagram stellt, es trägt die Kennzeichnung, die Artikel 50
verlangt, und hinter seinen Fenstern liegen Berge, die es an der Ostsee nicht
gibt. Damit belegt es beide Aussagen des Blocks auf einmal.

Wer die Bilder austauscht: die Kennzeichnung muss mit. Ein Deck, das die Pflicht
erklärt und selbst dagegen verstößt, verliert den Raum.

## Die EU-Zeichen auf der Kennzeichnungsfolie

Die beiden Zeichen auf Folie 20 sind die offiziellen Icons der EU-Kommission
für KI-Inhalte, veröffentlicht im Juli 2026: eines für vollständig KI-erzeugte,
eines für KI-veränderte Inhalte. Sie liegen als weißes SVG in
`assets/images/eu/`, die Vorlagen kamen aus
`EDGE/Clients/Bürokompetenz/Orga/ki-icons-fuer-eddie`.

Der QR-Code daneben führt auf die Downloadseite der Kommission:
`digital-strategy.ec.europa.eu/en/policies/eu-icons-labelling-ai-generated-content`.
Dort liegen alle drei Zeichen in vier Farbvarianten als SVG und PNG.

Der Code ist bewusst dunkel auf hell gehalten, obwohl das im schwarzen Deck
weniger elegant aussieht: helle Module auf dunklem Grund erkennen ältere
Scanner nicht zuverlässig, und dieser Code wird im Saal aus mehreren Metern
vom Beamer abfotografiert. Nach jeder Änderung mit `zxingcpp` gegenlesen,
ein QR-Code, der nicht scannt, fällt vor Publikum auf.

**Wichtig für die Aussage:** Die Verwendung der Icons ist freiwillig, die
Kennzeichnungspflicht dahinter nicht. Ein Satz wie unter dem Bild links reicht
genauso.

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
