# Digital Sparks – Home-Nachbau

Statischer Nachbau von https://www.digital-sparks.org/neuneuneu/home (Framer-Original), Section für Section.
Stil bleibt Digital Sparks (schwarz, Nib Pro + Roobert, Glas-Pills). Kein Sternenhimmel mehr im Hintergrund (auf Wunsch entfernt); Layouts orientieren sich an Referenzen.

## Stand: Hero in 4 umschaltbaren Varianten
Leiste ganz oben (`.variant-bar`) mit Toggle, Auswahl per URL-Hash (`#a`–`#d`) und localStorage.
Ziel aller Varianten: klar machen, dass Digital Sparks eine **App** ist (Stundenplan als App-UI).
- **A · Fenster** (Referenz: Platte): Nav-Leiste, Text linksbündig, darunter Browser-Fenster mit App
  (Sidebar + Stundenplan) auf Lila-Verlauf-Fläche, ragt in den Fold.
- **B · Zentriert** (Referenz: PayPal): alles zentriert, darunter iPad quer mit App.
- **C · Split** (Referenz: Discord): Text links, rechts gekipptes iPad + iPhone + schwebende Spark-Karten.
- **D · Claim** (Referenz: Area): nur „Jetzt ist Zukunft Thema.“ riesig, iPad auf farbiger Fläche.

- **E · Editorial** (Standard, wenn kein Hash gesetzt ist, aktueller Favorit): Claim „Jetzt ist / Zukunft / Thema.“
  links riesig (füllt ~halbe Breite), Lead + CTAs direkt darunter. Rechts **kein Tablet**, sondern stark
  gezoomter Stundenplan direkt auf Schwarz (`.e-plan`): Montag + halber Dienstag (Tage ausgeschrieben,
  linksbündig), 2 Sparks (Fit Check, Zukunftsforschung), übrige Fächer „Verantwortung“ und „Projekt“.
  Rechter Rand: Stufen-Blur (`.edge-blur`, 6 Streifen 3–18 px). Hover auf einen Spark: Rest wird weich +
  gedimmt (`:has()`), Spark bekommt 2-px-Ring.
- **F · Sparks**: wie E (Header hat Klassen `v-e v-f`, nutzt E-Styles), rechts statt Plan nur große
  Spark-Kacheln (`.e-tiles`): Zukunftsforschung hoch links, Fit Check + social.me_dia gestapelt rechts, angeschnitten.
- Nav: nur Logo + Burger. „Kostenlos nutzen“ (`.nav-cta`, absolut neben dem Burger) blendet sich erst
  ein, wenn der Primary-CTA der sichtbaren Hero-Variante unter die Nav gescrollt ist (`show-cta`, JS in onScroll).
  „Anmelden“ ist raus aus der Nav (gehört künftig ins Menü).
- Logo: Funke durch fetten Pixel-Funken ersetzt (`.logo-spark`, 9×9 Raster, 1,35× skaliert).
  Lila Starburst „FREE“ (`.logo-burst`) sitzt rechts neben dem Logo, überdeckt die Wortmarke nicht.
- „Deeper Learning“-Siegel unten rechts ist entfernt; dort steht „Frag Jessi“ jetzt von Anfang an.
- Lead E/F: „… passen. **Datensicher und europäisch souverän** [EU-Flagge s/w]“ (Flagge inline-SVG `.flag`:
  gefüllte weiße Fläche, kräftiger schwarzer Sternenkranz, 1,5em breit).
- Starburst-Form (FREE / wow!) ist kräftiger: 14 Zacken, große Mitte, damit der Text nicht über die Zacken läuft.
- E-Plan: Montag = Verantwortung · Tools of Tomorrow (2 × 90 Min) · Projekt; Dienstag = Fit Check
  (angeschnitten). Fächer grau flächig (`.e-slot--fill`, #3A393D). Karten-Sticker (Oval/Ticket) sind raus.
- „Deeper Learning“-Siegel unten rechts ist lila mit weißer Schrift und dreht sich.
- **Sticker-Set (SVG, `.stk` + `.slap`)** nach den Vorlagen aus dem Brand-Material:
  Starburst lila/„FREE“, Oval pink mit gelber Schrift/„Datensicher“, Siegel gelb mit Kreistext lila/
  „Deeper Learning“, Ticket grün mit Nib-Pro-Schrift lila/„Projekt-basiert“. Pfade generiert per
  Skript (Starburst/Siegel), Position + Kippung inline (`--w`, `--rot`, `--d`). „Slap“: kurz/hart ohne Bounce.
- Pixel-Funken am Claim entfernt (CSS `.pix` existiert noch, wird aktuell nicht genutzt).
- Lead-Text ohne „Kostenlos und datensicher“ (steckt jetzt im Logo-Sticker), direkt unter dem Claim.

**Favoriten: B · Zentriert und E · Editorial.** Gemeinsamer Stand:
- Claim nur „Jetzt ist Zukunft Thema.“ (LP/Statement-Größe). Eyebrow nur Text.
- Body: „… Kostenlos und datensicher.“ mit `.mark--lila` (kostenlos) / `.mark--pink` (datensicher),
  Unterstreichung zeichnet sich nach dem Reveal.
- Tablet zeigt eigenen Plan im Ur-Look (`tpl-ipad-plan`, Klassen `.ip-*`): ohne Sidebar, Zeitspalte und
  Statusleiste, schwarz, flach, Radien 32/24, „Do – Fr“ als Pill. Kippt auf Hover (`[data-tilt]`, nur `pointer: fine`).
- Sticker = Baustein `.bubble` (Sprechblase), `.bubble--lila` / `.bubble--pink`, gekippt über `--rot`,
  `--flip` spiegelt den Zipfel. Flach, erscheinen weich (`.pop`, `--d` = Delay), schweben 5 s.
- `tpl-copy` gilt für A–D, E hat eigene Copy im Markup.

## Neue Varianten G, H, I (auf Basis Editorial + Collage)
- **G · Inline** (`.v-g`): Claim über volle Breite, Spark-Cover stecken als Bild-Pills zwischen den Wörtern
  (`.g-pill`, Tools of Tomorrow / Zukunftsforschung / Fit Check). Hover: Pill geht auf, zeigt Titel + Dauer,
  Rest des Claims wird weich. Brandbook-Signatur: Caption „Lernen, was wirklich zählt.“ rechts oben (`.g-caption`).
- **H · Tafel** (`.v-h`): links Claim + Lead, rechts „Dienstag · Raum 204 · Klasse 9b“ (Manifest) als
  typografische Liste (`.h-list`). Zeilen rollen beim Laden rein (`roll-in`), Spark-Zeilen weiß, „jetzt“-Pill pink.
  Hover auf Spark-Zeile: Cover folgt der Maus (`.h-float`), Rest der Liste wird weich. Touch: Thumbnail in der Zeile.
- **I · Pinnwand** (`.v-i`): zentrierter Claim, 8 Spark-Karten als gekippte Collage rundherum (`.i-card`,
  Position `--x/--y`, Mobile `--mx/--my`, `.i-hide-sm`), „wow!“-Starburst auf Zukunftsforschung.
  Mit Maus ziehbar (Pointer-Events, `translate`), Klick ohne Ziehen öffnet den Spark. Auf Touch normale Links.
- **J · Tisch** (`.v-e .v-j`, nutzt E-Layout für Claim/Lead): rechts eine Tischszene in Draufsicht (`.j-scene`,
  Maße in `cqw`): Tablet mit Tools-of-Tomorrow-Seite der Lernplattform (Cover, Chips, Titel, „Spark starten“),
  darüber eine gezeichnete Hand (SVG, lila Ärmel) mit weichem Blur-Schatten, die alle 4 s auf den Button tippt;
  daneben Post-its („Was kann KI wirklich?“), Tesa-Rolle, Stift, Knete. Maus-Parallaxe über `--px/--py` und `--depth`.
- **K · Person** (`.v-e .v-k`): Claim „Jetzt ist / Zukunft / Thema“ (ohne Punkt, wie im Mockup), rechts die
  Illustration der Person mit Rucksack (`assets/person.png`, per Swift-Skript aus weißem Hintergrund freigestellt),
  groß, rechts/unten angeschnitten, schwebt. **Darunter eine eigene Section** (`.k-app`, auch Klasse `hero v-k`):
  Signatur „Komplett ready.“ + Caption „Du musst nur noch den Beamer anmachen.“, großes Tablet mit der
  Lernplattform-Oberfläche von Tools of Tomorrow (`.ka-*`: Phasen Intro/Discover/Create/Share, Schritte mit Minuten,
  Dock Spark/Einladen/Optionen/Handbuch/Verlassen). Aktiver Schritt füllt sich in 6 s und springt weiter, Klick
  setzt einen Schritt. Darunter 4 Fakten-Karten: Deeper Learning, Datensicher, Fertig geplant, Kostenlos.
  Scroll-Reveal über `.sr` + IntersectionObserver. Copy der Karten ist Platzhalter (keine erfundenen Fakten).
  Lücke zwischen Text und Figur: „Lernreise“-Route (`.k-route`, gestrichelter SVG-Pfad mit wandernden Strichen)
  zur Hand der Figur, entlang schweben Themen-Pills aus dem Brandbook-Wert „Mut“ (KI, Klima, Identität,
  Mentale Gesundheit, Demokratie) + Caption „Die Themen, die eh fällig sind.“ Mobile: Themen als Sticker-Reihe.
- **L · Tanz** (`.v-e .v-l`): wie K, aber mit der tanzenden Figur (`assets/person-dance.png`, `.l-person`), deren
  ausgestreckte Hand Richtung Claim zeigt. Figur groß und angeschnitten (`.l-person`, Breite 60vw, rechts −14vw, `top: 3%`):
  Oberkörper mit Zukunftsbrille neben dem Claim; über die Breite gesteuert, damit sie nie über dem Text liegt
  (geprüft 1280 / 1512 / 2000). Nach unten weich: progressiver Blur (`.l-fade`, drei maskierte Glasebenen) + Bildmaske.
  Ein Sticker („wow!“ neben dem Kopf), auf ≤900 px ausgeblendet.
  Keine App-Karte mehr im Hero. Subheader als technische Glas-Pill über dem Claim: grüner Status-Punkt,
  Versalien mit Laufweite, „LERNPLATTFORM / AB KLASSE 9“ (`.l-sub`).
  Lead: „Fertige Lernreisen, die in deinen Stundenplan passen und deine Klasse Schritt für Schritt führen. Datensicher …“
  Die App-Section aus K gilt auch für L (`class="hero v-k v-l v-m k-app"`).
- Nav läuft über die volle Breite (`.nav > .wrap { max-width: none }`), Logo größer (`clamp(200px, 14vw, 280px)`),
  dadurch bündig mit dem Claim auch im Widescreen.
- **M · Ordnung** (`.v-m`): aufgeräumte Version von L im 2-Spalten-Raster (`.m-grid`). Links Claim, Lead
  (Lernplattform-Variante aus L) und CTAs; rechts eine dunkle Bühne (`.m-stage`, Radius 32), deren Oberkante auf
  Höhe des Claims und Unterkante auf Höhe der Buttons liegt. Auf der Bühne: Figur mit gekreuzten Armen
  (`assets/person-stretch.png`) in voller Höhe rechts, Plattform-Karte gerade und vertikal zentriert, ragt über die
  linke Bühnenkante (Brücke zum Text). Ein Sticker („wow!“) an der Bühnenecke. Mobile: Figur oben, Karte darunter.
  App-Section aus K gilt auch für M (`class="hero v-k v-l v-m k-app"`).
- Zusätzliche Cover in `assets/`: Future Voices, POV: Demokratie, Make it circular, Mentale Gesundheit.

## Brandbook-Regeln (Brand Book 2.0, Okt. 2026), die hier gelten
- Schwarz + Sterne als Raum. Farbe klein (Sticker/Akzent), **keine Verläufe, keine farbigen Vollflächen**.
- Themenfarben: Gelb #F7FF1C (Text schwarz), Lila #6A00E0 (Text weiß), Pink #F981F9 (Text schwarz), Grün #59E686.
- Sticker: immer 5–15° gekippt, flach (kein Schatten), eine Fläche + eine Textfarbe, überlappt sein Element.
  Formen: Pill, Sprechblase, Starburst, Siegel, Ticket, Wolke. Rollen: Reaktion („wow!“) oder Fakt („kostenlos“).
- Bewegung: Schweben 3–6 s, 6–14 px, kein Bounce, keine Eigenrotation. Blur statt Schatten. Reduced Motion: alles steht.
- Radien: Flächen 32 px, Pills voll rund, verschachtelt innen = außen minus Padding. Keine Schatten.
- Buttons: Primary „Kostenlos loslegen“, Secondary „Sparks ansehen“ (Outline + Glas). Hover 2-px-Ring, Pressed .97, kein Wachsen.
- Schrift: Nib Pro 600 für Claims/Statements (LP/Statement 130/116 · 90/80 · 52/48), Roobert 400/650 für alles Funktionale.
- Sprache: „du“ klein, „Lehrkraft“, „Schüler*innen“, „Lernplattform“ (nicht „App“), „Spark/Lernreise“,
  keine Gedankenstriche, Zahlen als Ziffern („2 × 90 Minuten“).
- Noch nicht umgesetzt: Varianten A, C, D nutzen noch Verläufe/Schatten und „App“-Wording.

## Struktur
- `index.html` – alles inline. Gemeinsame Bausteine als `<template>`: `tpl-copy`, `tpl-app`, `tpl-plan`,
  `tpl-statusbar`; Platzhalter `data-tpl="…"` werden per JS eingesetzt (verschachtelt).
- Geräte-Screens (`.screen[data-w][data-h]`) rendern in fester Gerätegröße (iPad 1180×820, iPhone 390×844)
  und werden per ResizeObserver skaliert.
- `.compact` = Mobile-App-Layout (nur Mi + Do–Fr); im iPhone fest, in Variante A per matchMedia ≤640px.
- Animationen: `.reveal` (Blur-Reveal), `.rise` (von unten), `.slide` (von rechts), `.drop` (Sparks fallen
  in den Plan). Beim Variantenwechsel neu abgespielt (`play()`).
- `assets/` – Cover-Bilder, Avatar, Logo-SVG (inline eingesetzt), `fonts/` (vom Original)

## Offen (nächste Sections, Reihenfolge Original)
Video, Sparks Themen, So funkts, Kreativer Unterrichten, Statement Break, Noch Fragen, Über uns,
Möglich Macher. Menü-Panel (offen) ebenfalls offen. Eine Hero-Variante auswählen.

## Design-Tokens (vom Original)
- Hintergrund #000, Karten rgb(35,34,37), Glas rgba(51,51,51,.55) + blur(20px), Pills Radius 99
- Headline Nib Pro 600, UI Roobert 400/650

## Lokal starten
`python3 -m http.server 4388` (siehe `.claude/launch.json`). Geprüfte Breiten: XS 375, M 768, L 1280/1512, XL 2000. Hinweis: Browser cached hart → ggf. mit `?v=n` neu laden.
