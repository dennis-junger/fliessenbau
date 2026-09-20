# Fliesenatelier Berlin – Homepage

Statische Website ohne Build-Schritt: reines HTML, CSS und etwas JavaScript.
Die Startseite steckt komplett in `index.html` – Design-Tokens oben im `<style>`,
Sticky-Navigation mit Fortschrittsbalken, Reveal-Animationen beim Scrollen,
Rechtsseiten separat. Zum Ändern reicht ein Texteditor, es muss nichts kompiliert werden.

## Dateien

| Datei | Inhalt |
|---|---|
| `index.html` | Startseite: Hero, Leistungen, Atelier-Linie (Klassik/Design/Signature), Material & Direktimport, Handwerksdetails, Ablauf, Projekte, Wartung, Einsatzgebiet, Anfrageformular, Footer |
| `impressum.html` | Impressum (mit Platzhaltern) |
| `datenschutz.html` | Datenschutzerklärung (auf GitHub Pages + Google Fonts + mailto-Formular zugeschnitten) |
| `img/logo.svg` | Logo/Favicon |
| `img/muster-*.svg` | Sechs selbst erzeugte Fliesenmuster als Beispielbilder (Intarsie, Zellige, Marmor-Buchmatch, Ornament, Hexagon, Terrazzo) |
| `.nojekyll` | Schaltet die Jekyll-Verarbeitung auf GitHub Pages ab – die Seite wird 1:1 ausgeliefert |
| `MARKTANALYSE.md` | Wettbewerbsrecherche Berlin: Anzahl Anbieter, ihre Schlagwörter, Kundengewinnung, fünf unbesetzte Positionierungen |

## Noch einzutragen

Alle Stellen sind im Code mit `TODO` markiert (`grep -rn TODO .`):

- **Firmenname** – aktuell überall „Fliesenatelier Berlin“ (Nav, Footer, Titel, JSON-LD, Rechtsseiten)
- **Preise der Atelier-Linie** – drei `TODO €`-Felder in der Sektion „Atelier-Linie“. Ohne Preisanker verliert die Signature-Linie ihre Wirkung; ein „ab“-Preis filtert Anfragen vor
- **Telefonnummer** – `030 000 000 00` und die `tel:+493000000000`-Links
- **E-Mail** – `info@example.de`, auch die Konstante `EMPFAENGER` im Skript ganz unten
- **Adresse** – `Musterstraße 12, 10115 Berlin`
- **Domain** – `og:url` im `<head>`
- **Referenzprojekte** – die drei Karten unter „Zuletzt gelegt“
- **Impressum**: Handelsregister, USt-ID, Handwerkskammer, Handwerksrolle, Versicherung

## Positionierung

Die Seite ist bewusst nicht als „Fliesenleger in Berlin" gebaut – davon gibt es rund tausend,
und alle werben mit denselben Worten. Stattdessen: Fliesenatelier mit eigenem Direktimport,
mit sichtbarer Premium-Linie (Signature) für zahlungsbereite Kunden. Die Begründung und die
Wettbewerbsdaten stehen in `MARKTANALYSE.md`.

## Fotos einsetzen

Auf der Seite liegen aktuell selbst erzeugte Fliesenmuster als Beispielbilder.
Sie sind lizenzfrei, laden schnell und passen zum Thema – ersetzen aber keine
echten Fotos. Sobald welche da sind, einfach das `src` austauschen:

```html
<!-- vorher -->
<img src="img/muster-marmor.svg" alt="Marmor mit gespiegelter Maserung (Buchmatch)"
     width="900" height="1100" loading="lazy" decoding="async" />
<!-- nachher -->
<img src="img/projekt-1.jpg" alt="Fertiges Onyx-Bad mit hinterleuchteter Wand"
     width="1600" height="2000" loading="lazy" decoding="async" />
```

`width` und `height` immer mitangeben – sonst springt das Layout beim Laden.
Bilder vorher auf ca. 1600 px Breite verkleinern und als JPG speichern
(unter ~300 KB je Bild).

### Wichtig: die drei Projektkarten

Die Karten unter „Zuletzt gelegt“ tragen eine sichtbare Kennzeichnung
**Beispielbild**. Das muss so bleiben, solange dort keine echten eigenen
Projektfotos liegen – sonst behauptet die Seite Arbeiten, die es so nicht gab.
Beim Einsetzen echter Fotos das jeweilige
`<span class="beispiel">Beispielbild</span>` mit entfernen.

### Wenn du doch Stockfotos nehmen willst

Kostenlos und auch gewerblich nutzbar, ohne Namensnennungspflicht:

- [Unsplash](https://unsplash.com) – Unsplash-Lizenz
- [Pexels](https://pexels.com) – Pexels-Lizenz
- [Pixabay](https://pixabay.com) – Pixabay Content License

Brauchbare Suchbegriffe: `bathroom tiles`, `marble bathroom`, `terrazzo floor`,
`zellige`, `tiler working`, `mosaic tile`. Bilder herunterladen und nach `img/`
legen – nicht per Link einbinden, sonst geht die IP jedes Besuchers an den
Anbieter und die Datenschutzerklärung müsste ergänzt werden.

Auch hier gilt: Stockfotos gehören nicht in die Referenzen. Ein Kunde, der dort
ein fremdes Bad sieht, glaubt, es sei deines.

## Anfrageformular

Das Formular kommt ohne Server aus: Beim Absenden öffnet JavaScript das E-Mail-Programm
des Besuchers mit vorausgefüllter Nachricht. Das reicht für den Anfang, hat aber zwei Nachteile –
auf manchen Geräten ist kein Mailprogramm eingerichtet, und die Anfrage landet nicht automatisch
in einem Postfach.

Für echten Versand einen Formulardienst eintragen (z. B. Formspree, Basin, Web3Forms):

```html
<form id="anfrage" action="https://formspree.io/f/DEINE-ID" method="POST">
```

Danach den `mailto`-Block am Ende von `index.html` löschen und die Datenschutzerklärung
um den Dienst als Auftragsverarbeiter ergänzen.

## Veröffentlichen mit GitHub Pages

Einmalig einschalten – danach ist jeder Push auf `main` automatisch live:

1. Im Repository auf **Settings** (oben rechts im Reitermenü)
2. Links in der Seitenleiste auf **Pages**
3. Unter **Build and deployment → Source**: **Deploy from a branch**
4. Branch: **main**, Ordner: **/ (root)** → **Save**

Nach ein bis zwei Minuten läuft die Seite unter:

```
https://dennis-junger.github.io/fliessenbau/
```

Der Status des Deployments steht im Reiter **Actions**, und auf der Pages-Seite
erscheint oben ein grüner Kasten mit der fertigen Adresse.

### Eigene Domain

Eine Adresse wie `fliesenatelier-berlin.de` wirkt bei zahlungskräftigen Kunden
deutlich anders als eine `github.io`-Adresse. Einrichtung:

1. Domain beim Anbieter kaufen (Strato, IONOS, Namecheap …)
2. Beim Anbieter im DNS anlegen:
   - `CNAME` für `www` → `dennis-junger.github.io`
   - für die Domain ohne `www` vier `A`-Records auf
     `185.199.108.153`, `185.199.109.153`, `185.199.110.153`, `185.199.111.153`
3. In **Settings → Pages → Custom domain** die Domain eintragen und speichern
   (GitHub legt dabei automatisch eine `CNAME`-Datei im Repository an)
4. Sobald das Zertifikat ausgestellt ist, **Enforce HTTPS** anhaken

Danach in `index.html` noch `og:url` auf die echte Domain setzen.

## Lokal ansehen

```bash
python3 -m http.server 8000
# http://localhost:8000/
```
