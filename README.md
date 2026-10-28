# Waytide-Kacheln — Kartendaten für Waytide

Dieses Repository hält die Daten, gegen die
[Waytide](https://github.com/tobiasKlingl/Waytide) geprüft wird und die
die Waytide-App lädt. Es enthält **Daten, keinen Code**, und zwar als
Releases vier verschiedener Arten:

| Release | Inhalt |
|---|---|
| `kachelstand-…` | `.rd5`-Routingkacheln, bei selbst gebauten Ständen mit der Herkunftsliste `abdeckung.json` |
| `karte-…` | Detailkarten im Vektorformat (`.pmtiles`) |
| `adressen-…` | Adressblöcke der Ortssuche (`.wto`) |
| `messung-…` | Rohdaten einer Messung |

Die Lizenzangaben der Karten und Adressblöcke stehen in der
Beschreibung ihres Release; dieses README beschreibt die Routingkacheln.

---

## Herkunft und Lizenz

**Die Kacheln sind eine abgeleitete Datenbank im Sinne der ODbL.** Sie
enthalten Kartendaten von OpenStreetMap.

> Enthält Informationen von OpenStreetMap, die unter der
> [Open Database License 1.0](https://opendatacommons.org/licenses/odbl/1-0/)
> verfügbar gemacht werden.
> © [OpenStreetMap-Mitwirkende](https://www.openstreetmap.org/copyright)

**Diese Kacheln werden hiermit ebenfalls unter der ODbL 1.0
angeboten** (ODbL §4.4, Share-Alike). Herunterladen ist und bleibt
kostenlos (§4.6); eine Bezahlschranke davor gibt es nicht und darf es
nicht geben.

### Was in welcher Kachel steckt

| Herkunft | Lizenzen | Was zu nennen ist |
|---|---|---|
| unverändert von [`brouter.de/brouter/segments4/`](https://brouter.de/brouter/segments4/) | ODbL 1.0 | OpenStreetMap |
| selbst gebaut mit [`kacheln/deutschland_bauen.sh`](https://github.com/tobiasKlingl/Waytide/blob/main/kacheln/deutschland_bauen.sh) | ODbL 1.0 **und** CC BY 4.0, dazu die Bedingungen der AWS Terrain Tiles | OpenStreetMap, Sonny **und** die Quellen der AWS Terrain Tiles (unten) |

**Der volle Text der ODbL 1.0 steht in [`LICENSE`](LICENSE)** (aus der
SPDX-Lizenzsammlung).

**Welche das jeweils sind, sagt die Beschreibung des Releases** — dort
und nur dort, weil es von Release zu Release wechselt.

### Wenn Höhen von Sonny darin stecken

Kacheln, die wir selbst aus OSM-Daten und eigenen Höhenmodellen bauen,
tragen eine **zweite** Lizenz: Das Geländemodell stammt dann von
[Sonny](https://sonny.4lima.de/) und steht unter
[CC BY 4.0](https://creativecommons.org/licenses/by/4.0/). Sonnys
Bedingung lautet wörtlich:

> „Please mention my name (Sonny) and put a link to my Website
> (sonny.4lima.de)."

Für solche Kacheln gelten **beide** Lizenzen nebeneinander — wer nur
eine erfüllt, erfüllt keine.

**Verändert** (CC BY 4.0 verlangt, Änderungen anzugeben): Die Kacheln
tragen Höhen nur an den Knoten der Wege, im Höhenformat von `rd5`; wir
lesen sie dort aus Sonnys Geländemodell ab. Je Gradzelle stammt die Höhe
von Sonny oder aus den AWS Terrain Tiles (unten) — oder die Zelle trägt
gar keine Höhe.

### Wo Sonnys Geländemodell nicht hinreicht: AWS Terrain Tiles

Ein Teil der Zellen außerhalb von Sonnys Gebiet trägt Höhen aus den
[AWS Terrain Tiles](https://registry.opendata.aws/terrain-tiles/); die
übrigen (im deutschen Kachelsatz vor allem Meer mit Fähren und
Fahrrinnen) tragen gar keine Höhe. Welche Zelle woher stammt — `sonny`,
`aws` oder `keine` —, steht je Kachelstand in der Herkunftsliste
`abdeckung.json` (Feld `quelle` je Zelle); Zahlen nennt dieses README
bewusst nicht, damit es nicht neben der Liste veraltet. Die Terrain
Tiles verlangen diese Namensnennung ihrer Quellen (Wortlaut aus
[tilezen/joerd, `docs/attribution.md`](https://github.com/tilezen/joerd/blob/master/docs/attribution.md)):

```
* ArcticDEM terrain data DEM(s) were created from DigitalGlobe, Inc., imagery and
  funded under National Science Foundation awards 1043681, 1559691, and 1542736;
* Australia terrain data © Commonwealth of Australia (Geoscience Australia) 2017;
* Austria terrain data © offene Daten Österreichs – Digitales Geländemodell (DGM)
  Österreich;
* Canada terrain data contains information licensed under the Open Government
  Licence – Canada;
* Europe terrain data produced using Copernicus data and information funded by the
  European Union - EU-DEM layers;
* Global ETOPO1 terrain data U.S. National Oceanic and Atmospheric Administration
* Mexico terrain data source: INEGI, Continental relief, 2016;
* New Zealand terrain data Copyright 2011 Crown copyright (c) Land Information New
  Zealand and the New Zealand Government (All rights reserved);
* Norway terrain data © Kartverket;
* United Kingdom terrain data © Environment Agency copyright and/or database right
  2015. All rights reserved;
* United States 3DEP (formerly NED) and global GMTED2010 and SRTM terrain data
  courtesy of the U.S. Geological Survey.
```

**Die Engine, die die Kacheln liest**, ist eine Portierung von
[BRouter](https://github.com/abrensch/brouter) (MIT). Das Format `rd5`
stammt von dort.

---

## Wie man sie bezieht

**Über die Releases dieses Repositories.** Ein Release `kachelstand-…`
ist ein **Kachelstand**: ein Name für einen Kartenstand, mit allen
Kacheln als Anhang.

Aus einem Waytide-Klon heraus holt ein Aufruf die Prüfkacheln des Ports
— nur, was fehlt, und jede Datei gegen Bytezahl und SHA-256 geprüft:

```sh
./tools/kacheln_holen.sh
```

Von Hand, wenn man Waytide nicht daneben hat:

```sh
S=https://github.com/tobiasKlingl/Waytide-Kacheln/releases/download/<kachelstand>
curl -L -O "$S/E5_N45.rd5"
```

**Warum Releases und nicht `git clone`:** Auf `main` liegen als
Git-LFS-Objekte nur die zwei Prüfkacheln aus dem Schnitt von brouter.de
(`E5_N45.rd5`, `E5_N50.rd5`); die selbst gebauten Stände gibt es nur als
Release. Der LFS-Medienpfad zählt zudem gegen ein monatliches
Bandbreitenkontingent; Release-Anhänge tun das nicht. Zum **Beziehen**
also die Releases.

## Der Kachelstand ist gepinnt, und das mit Absicht

Waytide hält jeden Kachelstand, gegen den es prüft oder den die App
lädt, mit Name, Bytezahl und SHA-256 je Datei fest. Der Grund ist nicht
Pedanterie: Die Golden-Dateien und das Abnahmetor des Ports gehören zu
**genau einem** Kartenstand. Ein unbemerkter Kachelwechsel sieht aus wie eine
Regression der Engine, und diese Verwechslung hat schon einmal einen
Testlauf gekostet.

Deshalb: **ein Kachelstand, ein Release, ein Tag.** `main` bewegt sich,
ein Tag nicht.

## Was hier NICHT hingehört

Bauartefakte, Zwischenstände (`.hgt`, `.bef`, `.pbf`), Höhenrohdaten.
Hierher gehören fertige Erzeugnisse — die Release-Arten oben.
