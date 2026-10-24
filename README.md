# too many maps

Inoffizielle Fan-Karte mit Orten aus den Rabbit Holes des Podcasts **too many tabs** (Caro & Miguel, NDR). Klick auf einen Punkt zeigt Ort, Folge, eine Kurzinfo und ob man hinfahren kann.

## Dateien

| Datei | Inhalt |
|---|---|
| `index.html` | die komplette Seite (Leaflet, keine Straßenkarte, nur Länderflächen) |
| `data/places.json` | alle Orte – hier werden neue Orte ergänzt |
| `data/review.csv` | alle Folgen mit Entscheidung „auf der Karte ja/nein“ |
| `vendor/` | Leaflet, Leaflet.markercluster, topojson-client und Natural-Earth-Länder (world-atlas), lokal eingebunden, damit keine externen Server geladen werden |

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
 "episode": { "title": "tab a / tab b", "date": "2026-10-21", "url": "https://www.ndr.de/podcast/…" }
}
```

Koordinaten bekommt man z. B. per Rechtsklick in Google Maps / OpenStreetMap. `uncertain: true` blendet im Popup einen Hinweis ein, dass Zuordnung oder Lage nicht ganz sicher ist.

## Online stellen (GitHub Pages)

Repo → **Settings → Pages** → „Deploy from a branch“ → Branch `main`, Ordner `/ (root)`. Nach ein, zwei Minuten ist die Karte unter `https://<user>.github.io/toomanymaps/` erreichbar.

## Lokal ansehen

Die Seite lädt `data/places.json` per `fetch`, das klappt nicht beim Öffnen als Datei. Stattdessen:

```sh
python3 -m http.server
# dann http://localhost:8000 öffnen
```

---

Kein offizielles Angebot von NDR oder too many tabs. Kartendaten: [Natural Earth](https://www.naturalearthdata.com/) (gemeinfrei) über [world-atlas](https://github.com/topojson/world-atlas).
