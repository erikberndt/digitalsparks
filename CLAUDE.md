# Digital Sparks

Workshop-Materialien und Web-Applets für „Digital Sparks“. GitHub: `erikberndt/digitalsparks`.

## Struktur
- `applets/` – eigenständige Single-File-HTML-Applets (Spiele, Prototypen), ohne Build.
- `katalog/` – Übersichtsseite der Applets (`index.html`, Einträge im JS-Array mit `file`, `preview` aus `katalog/previews/`).
- `hours/` + `api/hours.js` – Digital Sparks Hours (Monatsplanung mit Stunden-Tracking).

## Branches
- `main` – Stand für das Deployment.
- `spielwiese` – Experimente und Prototypen.

## Applet: 3D-Charakterauswahl (`applets/game-3d-character-select.html`)
3-Stufen-Prototyp (Unit 1–2 / 3–4 / 5): Figur auf der Bühne anklicken → tritt vor → „Perspektive übernehmen“ → Kamera fährt in den Kopf → Ego-Perspektive mit Monolog (Web Speech API + Untertitel) und ablaufender Szene → 2 Micro-Decisions → +1 Signalpunkt. Stufe 3 komplett → 100 %-Feier → „Nächsten Zyklus starten“.
- Vanilla JS + Three.js r128 (cdnjs), alles im Speicher, keine Persistenz.
- Inhalte im Objekt `DATA`: `stages`, `characters` (look, `unlock`, `slot`, `pitch`, `steps[n]` mit preview, mood, monologue, `scene`, choices), `edges`.
- `scene`: `env` (`yard` | `class` | `room` + `night`), `cam`, `eye`, `look`, `npcs`, `beats[i]` je Monologzeile. Beat-Aktionen: `look`, `camWalk`, `walk`, `turn`, `wave`, `nod`, `laugh`, `camNod`, `phone`, `screen` (chat/feed/note/call), `wait`.
- Figuren: Alex (Rückzug, ab 1), Mia (neu hier, ab 1), Sam (Lösungsfigur, ab 2), Jo (Brückenbauer:in, ab 3). Inhalte auf Deutsch.
- Auch als Claude-Artifact veröffentlicht: https://claude.ai/artifact/Nv1SUADMBLfhGRh7kWm49U (die Artifact-Version hat keinen `<!doctype>`/Viewport-Kopf, den ergänzt das Artifact selbst).
- Lokal testen: `python3 -m http.server 8765` im Repo, dann `/applets/game-3d-character-select.html`.
