# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this is

Digital Sparks is a small library of standalone, embeddable HTML learning games ("Applets") for climate/sustainability education, built for kids/students. There is no build system, package manager, or server — every applet is a single self-contained `.html` file deployed as a static site on Vercel and embedded elsewhere (e.g. Framer) via `<iframe>`.

## Repo layout

- `applets/*.html` — one file per learning experience/game. Fully self-contained: inline `<style>` and inline `<script>` (IIFE), no external JS dependencies, no build step.
- `katalog/index.html` — the internal "backend" catalog UI (German) listing all applets with published/draft status and generating the iframe embed code for each. The applet list (name, icon, file, published flag, gradient/deco) is hardcoded in a JS array at the top of the `<script>` block in this file — **when adding or removing an applet, update this array**.
- `.vercel/` — Vercel project link (gitignored, not committed).

## Workflow for adding a new applet

The `katalog/index.html` "Add learning experience" modal describes the intended workflow verbatim (German UI text): a new applet is built via Claude Code, confirmed with the user before pushing, and after push it shows up in the catalog as an unpublished draft. Concretely, creating a new applet means:

1. Add `applets/<new-file>.html` as a new self-contained HTML file following the existing conventions (see below).
2. Add a corresponding entry to the `applets` array in `katalog/index.html`'s script (with `published: false` for a new/unreviewed applet).
3. Confirm with the user before pushing/deploying — do not push automatically.

## Conventions used across existing applets

- Language: all user-facing text is German (`<html lang="de">`).
- Retro pixel-art aesthetic: Google Fonts `Press Start 2P` (headings/UI chrome) + `VT323` (body text), loaded via the same `fonts.googleapis.com` `preconnect` + `css2` link pair in every file.
- CSS custom properties for the palette (`--bg`, `--panel`, `--ink`, `--accent`, `--gold`, `--teal`, etc.), varied per applet but following the same naming scheme.
- Hard drop-shadow / pixel-border look (`box-shadow: Npx Npx 0 #000`, thick solid borders) instead of soft/blurred shadows.
- All logic lives in one `(function(){ ... })();` IIFE per file; state as top-level `let`/`const` inside the closure; UI rendered by rebuilding `innerHTML` from a `render()` function rather than a framework.
- `<title>` follows the pattern `<Name> — Retro` (or `— Retro-Prototyp` for in-progress prototypes).
- No shared JS/CSS files, no cross-applet imports, no localStorage/postMessage/multiplayer wiring currently in use — each applet is fully independent (the catalog's "Multiplayer" toggle is present in the UI but disabled/non-functional).

## Running/testing locally

There is no build or dev server. Open any `applets/*.html` or `katalog/index.html` file directly in a browser (or serve the repo root with any static file server) to test.

## hours/ – internes Stunden-Tracking (kein Applet)

`hours/` ist eine interne Planungs- und Tracking-Seite (Digital Sparks Hours), kein Lern-Applet: nicht in `katalog/index.html` eintragen, eigene Gestaltung statt Retro-Look. Planungsdaten in `hours/plan.js`; die Ist-Stunden speichert die Vercel-Funktion `api/hours.js` in Upstash Redis (Env `KV_REST_API_URL`/`KV_REST_API_TOKEN`). Neue Arbeitspakete brauchen eine neue `id` in `plan.js` und denselben Eintrag in `IDS` in `api/hours.js`.

## sparksapp/ – UI-Konzepte für die Lernreise-App (kein Applet)

`sparksapp/` enthält Design-Explorationen für die Digital-Sparks-App (Lernreise-Übersicht, Inhalts-View, Team-Board, Conversion-Flow), Tablet quer 1180 × 820 und Mobile 390 × 844. Quelle ist der Claude-Design-Canvas https://claude.ai/artifact/M9PNGs5W78Jqdzwn6P6rio; `sparksapp/designs/*.dc.html` sind Kopien der Screens (brauchen die Canvas-Laufzeit `support.js`, laufen nicht direkt im Browser), `designs/canvas.json` die Anordnung, `assets/` die Bilder. Nicht in `katalog/index.html` eintragen, eigene Gestaltung statt Retro-Look (Newsreader + Manrope, schwarzer Grund, Akzent `#6E44D9`). Aktueller Stand ist Reihe J (`J1-*`, `J2-*`); Details in `sparksapp/README.md`.

## Applet: 3D-Charakterauswahl (`applets/game-3d-character-select.html`)

3-Stufen-Prototyp (Unit 1–2 / 3–4 / 5): Figur auf der Bühne anklicken → tritt vor → „Perspektive übernehmen“ → Kamera fährt in den Kopf → Ego-Perspektive mit Monolog (Web Speech API + Untertitel) und ablaufender Szene → 2 Micro-Decisions → +1 Signalpunkt. Stufe 3 komplett → 100 %-Feier → „Nächsten Zyklus starten“.
- Vanilla JS + Three.js r128 (cdnjs), alles im Speicher, keine Persistenz.
- Inhalte im Objekt `DATA`: `stages`, `characters` (look, `unlock`, `slot`, `pitch`, `steps[n]` mit preview, mood, monologue, `scene`, choices), `edges`.
- `scene`: `env` (`yard` | `class` | `room` + `night`), `cam`, `eye`, `look`, `npcs`, `beats[i]` je Monologzeile. Beat-Aktionen: `look`, `camWalk`, `walk`, `turn`, `wave`, `nod`, `laugh`, `camNod`, `phone`, `screen` (chat/feed/note/call), `wait`.
- Figuren: Alex (Rückzug, ab 1), Mia (neu hier, ab 1), Sam (Lösungsfigur, ab 2), Jo (Brückenbauer:in, ab 3). Inhalte auf Deutsch.
- Auch als Claude-Artifact veröffentlicht: https://claude.ai/artifact/Nv1SUADMBLfhGRh7kWm49U (die Artifact-Version hat keinen `<!doctype>`/Viewport-Kopf, den ergänzt das Artifact selbst).
- Katalog-Eintrag `charselect` („Perspektiv-Wechsel 3D“, Entwurf), Vorschau `katalog/previews/charselect.png` (960×600, per Headless-Chrome von `…#stufe-3` gerendert).
- URL-Hash `#stufe-2` / `#stufe-3` startet direkt in dieser Stufe.
- Lokal testen: `python3 -m http.server 8766` im Repo, dann `/applets/game-3d-character-select.html` bzw. `/katalog/`.
