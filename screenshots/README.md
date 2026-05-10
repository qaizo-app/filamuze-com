# Landing page screenshots

Drop the eight app screenshots here, named exactly as below. The
landing's HTML references these paths (`/screenshots/01-...`) when
deployed to filamuze.com — keep the filenames stable so the redesign
doesn't break.

| File | Captures |
|---|---|
| `01-spool-detail.jpg` | Spool detail with weight + drying status (Sunlu PETG closeup) |
| `02-add-spool.jpg` | Add spool form with Scan-label CTA + material chips |
| `03-nfc-empty.jpg` | NFC tab idle state ("Tap a tag" + Scan/Write buttons) |
| `04-nfc-pair.jpg` | NFC pair flow — "New tag" with UID + spool picker list |
| `05-spool-list-grid.jpg` | Main list, grid view, 2×2 progress rings (PETG filter) |
| `06-stats.jpg` | Stats screen — total kg + by-material + by-colour bars |
| `07-spool-list.jpg` | Main list, line view with "Good evening" hero |
| `08-spool-detail-photo.jpg` | Spool detail with full photo of the actual reel |

Source format: JPG (Android phone screenshot, 1080×2109). The landing
uses `<img>` tags with CSS-driven sizing, so don't pre-resize — keep
originals so we can serve crisp images on high-DPI screens.

## What NOT to put here

- App icons → those live in [`docs/icon-variants/`](../../icon-variants/)
- Marketing banners → [`docs/marketing-assets/`](../../marketing-assets/)
- Screenshots from a competitor → don't ship those at all
