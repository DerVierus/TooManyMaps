# too many maps

Inoffizielle Fan-Karte mit Orten aus den Rabbit Holes des Podcasts **too many tabs** (Caro & Miguel, NDR). Klick auf einen Punkt zeigt Ort, Folge, eine Kurzinfo und ob man hinfahren kann.

## Dateien

| Datei | Inhalt |
|---|---|
| `index.html` | die komplette Seite (Leaflet + OpenFreeMap-Vektorkarte, Popups im Browserfenster-Look) |
| `data/places.json` | alle Orte – hier werden neue Orte ergänzt |
| `data/review.csv` | alle Folgen mit Entscheidung „auf der Karte ja/nein“ |
| `data/atlantis.json` | alle Themen ohne echten Ort (300 Tabs) – liegen gesammelt in **Atlantis** |
| `vendor/` | Leaflet, Leaflet.markercluster, MapLibre GL und das MapLibre-Leaflet-Plugin, lokal eingebunden |

## Neuen Ort eintragen

In `data/places.json` einen Eintrag anhängen:

```json
{
 "id": 89,
 "name": "Name des Ortes",
 "region": "Stadt, Land",
 "lat": 52.52,
 "lng": 13.405,
 "topic": "tab-titel",
 "info": "Ein, zwei eigene Sätze, worum es geht.",
 "visit": "Kann man hin? Museum, frei zugänglich, nicht mehr existent …",
 "uncertain": false,
 "wiki": "de:Artikelname",
 "image": { "src": "https://upload.wikimedia.org/…/320px-….jpg", "page": "https://de.wikipedia.org/wiki/…", "article": "…" },
 "episode": { "title": "tab a / tab b", "date": "2026-10-21", "url": "https://www.ndr.de/podcast/…" }
}
```

Koordinaten bekommt man z. B. per Rechtsklick in Google Maps / OpenStreetMap. `uncertain: true` blendet im Popup einen Hinweis ein, dass Zuordnung oder Lage nicht ganz sicher ist.

`image` ist optional: das Vorschaubild des Wikipedia-Artikels (`https://<sprache>.wikipedia.org/api/rest_v1/page/summary/<Artikel>` → `thumbnail.source`). Ohne Bild zeigt das Popup einen bunten Platzhalter.

## Atlantis

Themen ohne echten Ort landen in Atlantis (Anspielung auf die Live-Tour „Die Vampir-Piraten von Atlantis“), einem Punkt mitten im Atlantik (33° N, 27° W). Ein Klick darauf öffnet eine durchsuchbare Liste aller Atlantis-Tabs. Der zweite Tab im Fenster eines Ortes führt immer zum anderen Thema derselben Folge – zu einem echten Ort oder nach Atlantis.

Neuer Atlantis-Tab in `data/atlantis.json`:

```json
{ "id": "a301", "topic": "tab-titel", "info": "Ein, zwei eigene Sätze.", "episode": { "title": "tab a / tab b", "date": "2026-10-28", "url": "https://www.ndr.de/podcast/…" } }
```

Bekommt ein Atlantis-Thema später doch einen echten Ort, den Eintrag aus `atlantis.json` löschen und in `places.json` anlegen.

## Easter Eggs

Auf der Karte sind zehn Easter Eggs versteckt (🥚-Zähler in der Seitenleiste, mit Hinweisen). Gefundene Eier merkt sich der Browser. Der Code steht in `index.html` unter „Easter Eggs“.

## Online stellen (GitHub Pages)

Repo → **Settings → Pages** → „Deploy from a branch“ → Branch `main`, Ordner `/ (root)`. Nach ein, zwei Minuten ist die Karte unter `https://<user>.github.io/toomanymaps/` erreichbar.

## Lokal ansehen

Die Seite lädt `data/places.json` per `fetch`, das klappt nicht beim Öffnen als Datei. Stattdessen:

```sh
python3 -m http.server
# dann http://localhost:8000 öffnen
```

---

## Externe Dienste

- **Karte:** [OpenFreeMap](https://openfreemap.org) (kostenlos, ohne API-Key), Daten © [OpenStreetMap](https://www.openstreetmap.org/copyright)-Mitwirkende, [OpenMapTiles](https://www.openmaptiles.org/).
- **Fotos:** werden direkt von Wikimedia (upload.wikimedia.org) geladen; jedes Bild verlinkt auf seinen Wikipedia-Artikel, wo Urheber:in und Lizenz stehen.

Beim Öffnen der Seite lädt der Browser also Kacheln von OpenFreeMap und Bilder von Wikimedia.

Kein offizielles Angebot von NDR oder too many tabs.
