# sparksapp – UI-Konzepte für die Digital-Sparks-App

Design-Exploration für die Lernreise-App von Digital Sparks (Tablet quer 1180 × 820 und Mobile 390 × 844).
Entstanden als Claude-Design-Canvas „Climate CO₂llaboration – Mobile Journey“:
https://claude.ai/artifact/M9PNGs5W78Jqdzwn6P6rio

Der Canvas bleibt die lebende Version (klickbar, mit Tweaks). Dieser Ordner ist eine Kopie der Quellen
als Ausgangspunkt für die Umsetzung.

## Inhalt

- `designs/*.dc.html` – ein Screen pro Datei (Design-Component-Format des Canvas).
- `designs/canvas.json` – Anordnung, Titel und Gruppierung aller Screens auf dem Canvas.
- `assets/` – Bilder, die im Canvas als Uploads eingebunden sind:
  - `kampagne-foto.jpg` → in `K-Kampagne.dc.html` als `/_blob/03ed166d605c167c70bd4e345a3d504a`
  - `socialmedia-bahn.jpg` → in `H0-Start.dc.html` als `/_blob/4e2fef3cde788cb96082f608040203f6`

## Varianten-Übersicht

| Reihe | Dateien | Idee |
|---|---|---|
| A–C | `Main`, `Phasen`, `Sternbild`, `Tablet-*` | Erste Lernreise-Übersichten: Pfad, Phasen-Tabs, Sternbild-Karte |
| D | `D-*` | Phasen als untere Leiste, Showroom & Bibliothek vorne, Rest unter „Werkzeuge“ |
| E | `E-*` | Quick Fix: bestehendes Tablet-Layout fürs Handy; Kapitel öffnen Unterkapitel |
| F / K | `F1`–`F4`, `K-Kampagne` | Conversion-Flow mobil: Kampagne → Lernreise → Anmelden → Registrieren → Weiter am Tablet |
| G | `G-*` | Reise-Karte mit Phasen unten, Station als Fenster |
| H | `H0`–`H4` | Team-Board als zentraler Ort; Discover/Create/Share docken an; Start-Moment |
| L | `L1`, `L2` | Lagerfeuer (Ankommen) & Labor (Board mit KI-Laborant) |
| J | `J1-*`, `J2-*` | **Aktueller Stand:** Lernreise mit Etappen-Bentos (Größe = Zeit), Lehrkraft-Ansicht, Inhalts-View mit Breadcrumb, Seiten-Stepper, Wahl-Wegen und Übersicht-Overlay |

## Struktur-Modell (Reihe J)

Kurs → 3 Phasen (Discover, Create, Share) → 1–5 Etappen → 1–8 Stationen → 1–8 Seiten.
Apps (Bibliothek, Showroom, Spark, Handbuch; für Lehrkräfte zusätzlich Klassen-Apps) liegen quer dazu.
Etappen-/Stationsnamen und Zeiten in J sind Beispielwerte.

## Hinweise zum Format

Die `.dc.html`-Dateien brauchen die Laufzeit des Canvas (`./support.js`) und laufen nicht direkt im Browser.
Markup steht in `<x-dc>`, Logik in `<script type="text/x-dc">` (`class Component extends DCLogic`, `renderVals()`);
`{{…}}` sind Platzhalter, `<sc-for>`/`<sc-if>` Schleifen und Bedingungen. Für die Umsetzung als echte App
dienen sie als Vorlage für Layout, Farben, Typo und Zustände.

Look: schwarzer Grund mit Sternen, Newsreader (Serif, Titel) + Manrope (Sans, UI), Akzent `#6E44D9`,
Hell-Lila `#C9B6FF`, Lehrkraft-Gelb `#FFE27A`.
