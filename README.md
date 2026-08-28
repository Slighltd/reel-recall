# Reel Recall v0.6.0

Production-oriented static web game with all 54 local MP3 files imported and normalized.

## Game Session Controls

### Next Round
**Next Round** advances the existing game to another random unused track from the selected era.

It preserves:
- contestant/team scores
- contestant/team names
- game mode
- era selection
- clip and scoring settings
- used-song history, so tracks do not repeat until the eligible pool is exhausted

Keyboard shortcut: `N`

### New Game
**New Game** starts a fresh game session and is confirmation-protected to prevent an accidental reset.

It resets:
- all scores to zero
- the round counter to zero
- the current song/round
- used-song history

It intentionally preserves:
- contestant/team names and count
- team/player setting
- game mode
- era selection
- clip length
- score increment

Keyboard shortcut: `G`

## Player Display

Reel Recall now includes a separate player/team-facing display at `public/player.html`.

From the host interface, select **Player Display** to open the display in a separate browser window. The host can move that window to a TV, projector, or second monitor while retaining all controls privately on the host screen.

The Player Display mirrors only the live round stage:

- round era and round status
- current prompt
- clue/song/film information appropriate to the active game mode
- artist/context line
- clip progress and timer
- playback state
- answer reveal

The Player Display intentionally does **not** show:

- contestant/team scores
- Settings
- Mode Selection
- Era Selection
- Song Selection
- New Game / Next Round controls
- Reveal / Replay controls

Audio continues to play from the **host window only**. The player-facing display mirrors playback status and progress without starting a second audio stream, preventing echo or duplicated playback.

### Display synchronization

The host and player windows synchronize over the same Cloudflare origin using `BroadcastChannel`, with `localStorage` and `window.postMessage` fallbacks.

The Player Display receives the current state immediately when opened and continues updating during playback, pause, round changes, mode changes, answer reveal, and New Game resets.

Player Display convenience controls:

- `F` toggles fullscreen from the player window
- double-clicking the player stage also toggles fullscreen

Host shortcut:

- `D` opens/focuses the Player Display

## v0.6.0 Release Notes

- Added a dedicated **Player Display** pop-out window.
- Added `public/player.html` as the player/team-facing stage.
- Added live same-origin synchronization between host and player displays.
- Player view mirrors only current-round information and never exposes host settings, song-selection controls, or scores.
- Player view respects **Name the Movie**, **Name the Song**, and **Double Recall** concealment rules.
- Answer reveals, playback status, and clip progress are synchronized automatically.
- Audio remains host-side only to prevent duplicate playback.
- Added host **Player Display** button and `D` keyboard shortcut.
- Added `F` / double-click fullscreen support within the player display.
- Synchronized semantic version references to **v0.6.0**.
- Preserved all 54 audio tracks, existing track mappings, Cloudflare Wrangler configuration, and fullscreen-safe screen buffer.

## v0.5.1 Release Notes

- Changed the host-strip **Songs** control to the static label **Song Selection**.
- Removed the active/current song title from the host strip.
- Prevents accidental answer disclosure in **Name the Song** and **Double Recall** modes.
- Synchronized the runtime `VERSION` constant and semantic version references to **v0.5.1**.
- No gameplay logic, audio files, track mappings, Wrangler configuration, or deployment structure were changed.

## v0.5.0 Release Notes

- Added distinct **New Game** and **Next Round** workflows.
- Added confirmation protection for **New Game**.
- **Next Round** now clearly means advance within the current game without resetting scores.
- Added `G` keyboard shortcut for New Game and retained `N` for Next Round.
- Synchronized semantic versioning across `public/index.html`, `README.md`, `package.json`, and `public/data/playlist.yaml`.
- Preserved the v0.4.3 fullscreen-safe perimeter buffer.
- No audio files, track mappings, Wrangler configuration, or Cloudflare deployment structure were changed.


## Library
- 1980s: 20 tracks
- 1990s: 18 tracks
- 2000s+: 16 tracks
- Total: 54 tracks

## Track change
`You Could Be Mine` / *Terminator 2* was replaced with **Hedwig's Theme — John Williams — Harry Potter and the Sorcerer's Stone (2001)**.
Per the project organization, Hedwig's Theme is intentionally classified in the **1990s** game era.

## Audio convention
Every track is stored as:

`audio/<track-id>.mp3`

The browser manifest in `data/tracks.js` and source manifest in `data/playlist.yaml` already point to these files.

`data/audio-import.csv` records every original uploaded filename and its normalized site filename.

## Deployment
This is a static site. Upload the repository contents to GitHub/Cloudflare Pages. Because the repository contains commercial music files, only deploy the audio in a context where you have the necessary rights/permission to distribute or serve those files.


## Cloudflare Workers deployment

This release is structured for Cloudflare Workers Static Assets.

Repository layout:

```text
reel-recall/
├── wrangler.jsonc
├── package.json
├── .gitignore
├── README.md
└── public/
    ├── index.html
    ├── player.html
    ├── data/
    └── audio/
```

### Automatic Git deployment

1. Push this repository to GitHub.
2. In Cloudflare, open **Workers & Pages**.
3. Choose **Create application** → **Import a repository**.
4. Select the Reel Recall GitHub repository.
5. The Worker name must match `reel-recall` from `wrangler.jsonc`.
6. Leave the build command blank.
7. Use the default deploy command: `npx wrangler deploy`.
8. Set the production branch to `main`.
9. Save and deploy.

After the Git integration is connected, every push to `main` automatically deploys the updated site.

### Local commands

```bash
npm install
npm run dev
npm run deploy
```

### Custom domain

Do not add a `routes` entry to `wrangler.jsonc` until the final Reel Recall domain is chosen.
Configure the final custom domain in Cloudflare, then the Apogee Games index can link to it.
