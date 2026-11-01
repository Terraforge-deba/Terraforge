# TERRAFORGE

**Explore · Discover · Mine.** Terraforge is a voxel geoscience field adventure you play in the browser. You can build and survive the night. You can also take a mineral (gold, tin, lithium, coal or iron ore) through a 12-stage exploration-to-mining campaign, from desk study to mine closure.

![Terraforge world](docs/world.jpg)

| Campaign map | Drilling log | Split screen |
|---|---|---|
| ![map](docs/campaign-map.jpg) | ![drilling](docs/drilling.jpg) | ![split](docs/split-screen.jpg) |

## Features

- **Ways to play:** Expedition mode (hazards, health, Night Walkers) or Sandbox mode (free building, flying).
- **Building:** crafting, a day–night cycle, sound, and lanterns.
- **Campaign:** desk study, remote sensing, mapping (compass-clinometer), geochemistry with QA/QC, geophysics, drilling, a JORC-style resource estimate, feasibility, EIA/CDA and mining lease, mining, processing, and closure.
- **Controls:** keyboard and mouse, PS4 controller (Bluetooth), and phone or tablet touch controls.
- **Multiplayer:** two-player split screen on one device.
- **Accounts:** players register and sign in. The superadmin approves players and manages accounts.
- **Narration:** the superadmin's recorded voice guides players, and live commentary works too.

## How this repository works

```
index.html            ← the whole game (same file as Index.html in Apps Script)
config.js             ← your Apps Script web-app link goes here
manifest.webmanifest  ← lets players install Terraforge on phones/tablets
icons/  og-image.jpg  docs/
apps-script/Code.gs   ← the server (accounts, saves, voice) — runs in Google Apps Script
apps-script/Index.html
```

GitHub Pages hosts the game. Google Apps Script stores the accounts, worlds and voice clips in your Google Drive. Both links share the same data.

## Set up (about 10 minutes)

### 1 · The server (Google Apps Script)

1. Go to [script.google.com](https://script.google.com) and click **New project**. Paste `apps-script/Code.gs` into `Code.gs`.
2. Click **File → New → HTML file**, name it `Index`, and paste `apps-script/Index.html` into it.
3. In `Code.gs`, check `const SUPERADMIN = 'dexter';`. That is the username that becomes superadmin.
4. Click **Deploy → New deployment → Web app** and set:
   - **Execute as:** Me
   - **Who has access:** Anyone

   Click **Deploy**, approve the permissions, and **copy the Web app URL**. It ends in `/exec`.

### 2 · The website (GitHub Pages)

1. On GitHub, create a new **public** repository, for example `terraforge`.
2. Click **Add file → Upload files** and drag in **everything in this folder**, including the `.nojekyll` file. Then click **Commit changes**.
3. Open `config.js` on GitHub, click ✏️ **Edit**, and paste your `/exec` link between the quotes:
   ```js
   window.TERRAFORGE_API = 'https://script.google.com/macros/s/XXXXXXXX/exec';
   ```
   Then click **Commit changes**.
4. Go to **Settings → Pages → Build and deployment** and set:
   - **Source:** Deploy from a branch
   - **Branch:** `main`, folder `/ (root)`

   Click **Save**. After about a minute your game is live at:
   `https://<your-username>.github.io/terraforge/`

### 3 · Connect the two (for the microphone button)

1. In Apps Script, set `const HOSTED_URL = 'https://<your-username>.github.io/terraforge/';`
2. Click **Deploy → Manage deployments → ✏️ → Version: New version → Deploy**.

### 4 · First sign-in

Open your GitHub link and **register with the superadmin username first**. After that:

- New players register on the same page.
- You approve them under **Menu → 👑 Players**.
- To install Terraforge as an app, use **Add to Home Screen** on phones, or the install icon in Chrome's address bar on desktop.

## Updating the game later

1. Replace `index.html` in this repository with the new `Index.html`, renamed to `index.html`. Also update the copies in `apps-script/`.
2. If `Code.gs` changed, paste it into Apps Script and deploy a **New version**. Your `/exec` link stays the same.

GitHub Pages refreshes within a minute or two. Players may need to reload the page.

## Notes

- **Where data lives:** accounts, saved worlds and voice clips are in your Google Drive, in the folders `BlockWorld Accounts`, `BlockWorld Saves` and `BlockWorld Voice`.
- **Passwords:** they are stored only as salted hashes, never as text.
- **The `/exec` link is public.** That is normal: everything behind it needs a signed-in account.
- **If `config.js` is left empty,** the game still runs, but offline only. Worlds stay in that browser and there are no accounts.
- **Prices, costs and royalty rates** in the campaign are simplified game values for teaching.

---
© Dexter Roy GeoConsult Limited (DRGL). All rights reserved.
