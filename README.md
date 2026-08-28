# Reel Recall v0.4.2

Production-oriented static web game with all 54 local MP3 files imported and normalized.

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
