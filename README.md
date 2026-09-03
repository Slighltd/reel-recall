# Apogee Games Main Site v1.11.0

Static deployment patch for https://apogeegames.slighltd.org/.

## Purpose

The main Apogee Games site is the network landing page for the three current game lines:

- Awake in the Black
- Cultists & Classrooms
- Star Wars: Flow of the Force

Each current game routes to a dedicated resource hub. The Design Archive and Bonus Shelf remain collected on the main Apogee Games site.

## Bonus Shelf

The Bonus Shelf now contains three peer projects:

- Golf: It’s a Good Game v4.1.0, bundled locally at `bonus/golf-its-a-good-game/index.html`
- Boggle v1.1.0, bundled locally at `bonus/boggle/index.html`
- Reel Recall, hosted externally at https://reel-recall.slighltd.org/

## Deployment

Replace the root `index.html` and `README.md` in the existing Apogee Games repository with the files in this patch.

This patch assumes the v1.10.0 repository structure is already present, including the existing Boggle bundle at `bonus/boggle/index.html`.

No `wrangler.jsonc` change is required for Reel Recall because the game is linked to its existing external Cloudflare-hosted site.

## External game hubs

- Awake in the Black: https://awake.slighltd.org/
- Cultists & Classrooms: https://cult.slighltd.org/
- Star Wars: Flow of the Force: https://flow.slighltd.org/
- Reel Recall: https://reel-recall.slighltd.org/

## Current release

**Site build:** v1.11.0  
**Release date:** 2026-09-03

### v1.11.0

- Added Reel Recall to The Bonus Shelf.
- Added a direct external launch button for `https://reel-recall.slighltd.org/`.
- Preserved Golf and Boggle as equal Bonus Shelf projects.
- Updated the Publishing Console, footer build label, Bonus copy, and site changelog to v1.11.0.
- No Wrangler routing change required.

### v1.10.0

- Added Boggle v1.1.0 as a bundled local browser game.
- Refactored the Bonus section into The Bonus Shelf to support multiple standalone projects.
