# hours – Digital Sparks Hours

Monatsplanung und geteiltes Stunden-Tracking für ein Teammitglied (Okt 2026 – Jan 2027).
Erreichbar unter `/hours/`. Nicht im Katalog verlinkt, aber öffentlich für alle mit Link.

- `plan.js` – Planungsdaten. Für Planänderungen nur diese Datei anpassen.
  Die `id` eines Pakets nicht ändern, sonst beginnt sein Zähler bei 0.
  Neue Pakete zusätzlich in `api/hours.js` unter `IDS` eintragen.
- `app.js` – Darstellung und Tracking
- `styles.css` – Gestaltung
- `../api/hours.js` – Vercel-Funktion, speichert die Stunden in Upstash Redis

## Speicher einrichten (einmalig)

Vercel-Dashboard → Projekt digital-sparks → Storage → Upstash for Redis anlegen und mit dem Projekt verbinden.
Danach neu deployen. Die Funktion liest `KV_REST_API_URL` / `KV_REST_API_TOKEN`
(oder `UPSTASH_REDIS_REST_URL` / `UPSTASH_REDIS_REST_TOKEN`).
