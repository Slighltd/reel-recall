# Reel Recall v0.8.1

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
- live contestant/team score strip
- answer reveal

The Player Display intentionally does **not** show:

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

## v0.8.1 Release Notes

- Added **Tokyo Drift (Fast & Furious)** by **Teriyaki Boyz** from *The Fast and the Furious: Tokyo Drift* (2006).
- Added the track to the **2000s+** pool.
- Standardized the source audio filename as `audio/tokyo-drift-tokyo-drift-fast-and-furious.mp3`.
- Updated the complete Reel Recall library from **120 to 121 tracks**.
- Updated `tracks.js`, `playlist.yaml`, and `audio-import.csv`.
- Synchronized semantic version references to **v0.8.1**.
- No gameplay, Disney-theme logic, Player Display behavior, or Wrangler configuration was changed.

## v0.8.0 Release Notes

### Expanded music library
Imported and normalized **66 new MP3 files** from the supplied update packages:

- 1980s Update: 10 tracks
- 1990s Update: 14 tracks
- 2000s+ Update: 13 tracks
- Disney Update: 29 tracks

The complete Reel Recall library now contains **120 tracks**.

All imported audio was renamed to the established convention:

`audio/<track-id>.mp3`

The complete original-to-site filename mapping is recorded in `public/data/audio-import.csv`.

### Disney theme
**Disney** is now available in the existing Era selector and the Song Selection filter.

Disney is implemented as a theme rather than replacing chronological era metadata. A Disney track can therefore belong to both:

- its chronological era, such as `1990s`
- the `Disney` theme

This allows the normal decade games to retain Disney songs while also providing a dedicated Disney-only game.

The Disney pool contains:
- all 29 tracks from the new Disney package
- existing Reel Recall songs from Toy Story, Aladdin, Beauty and the Beast, The Lion King, Pocahontas, Mulan, Tarzan, A Goofy Movie, and Cars

Current Disney theme pool: **45 tracks**.

Disney films released before 1980 retain `Pre-1980` as chronological metadata. They are available through **All Eras** and **Disney**, but no separate Pre-1980 button has been added.

### Data model
Track records now support a `themes` array:

```json
{
  "era": "1990s",
  "themes": ["Disney"]
}
```

This keeps era and theme selection additive and makes future themed pools possible without duplicating tracks or audio files.

### Semantic version
Updated to **v0.8.0** across the host interface, Player Display, README, `package.json`, and playlist manifest.

Cloudflare/Wrangler configuration and all existing v0.7.0 gameplay features remain unchanged.

## v0.7.0 Release Notes

### Host answer key
The host stage now always shows a compact private answer key containing the **song, artist, and movie** for the loaded round. This information is never transmitted to the Player Display unless the answer is formally revealed.

### Five-second answer timer
A new **Start 5s Timer** host control is available whenever a round is loaded.

- If the music is currently playing, starting the answer timer automatically pauses it.
- The Player Display shows only a large floating `5 → 4 → 3 → 2 → 1 → 0` countdown.
- Pressing the timer button again while active resets it to five seconds.
- Resuming/replaying the song, changing rounds, revealing the answer, or starting a New Game clears the answer timer.
- Host shortcut: `T`.

### Clip lengths
Available clip-duration settings are now:

- 5 seconds
- 10 seconds
- 15 seconds
- 20 seconds
- 30 seconds
- 45 seconds
- 60 seconds

### Player score header
The Player Display now includes a small live score strip showing the active team/player names and current scores. Score and name changes made on the host are synchronized immediately.

### Pause/resume behavior
Paused music now resumes from the actual audio position where it was stopped rather than calculating a new start from the beginning of the clip.

### Previous Track
A new **Previous Track** control lets the host move backward through the current game's round history.

- Returning to a previous round does not reset scores.
- **Next Round** moves forward through existing history first, then selects a new random unused track.
- New Game clears round history.
- Host shortcut: `P`.

### Viewport-fit refactor
The host and player game surfaces are now explicitly bounded to the available browser viewport.

- Main game screens use no page-level scrolling.
- Header, controls, stage, scoreboard, footer, and player display scale vertically as well as horizontally.
- Narrow screens use compact multi-row controls and a compressed horizontal scoreboard.
- Configuration overlays may still scroll internally when necessary; the active game surface does not.

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
