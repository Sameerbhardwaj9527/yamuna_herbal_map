# 🌿 Atamnirbhar Society — Farmer Interactive Map

An interactive map for **~1000 farmers** across Uttarkashi, Uttarakhand — built for the Atamnirbhar Society NGO project.

## ✨ Features

- 🗺 **Live data** — fetches directly from your Google Sheet (no manual CSV export needed)
- 📍 **Colour-coded pins** by Block, with animated popup cards
- 👤 **Farmer detail cards** — name, village, block, tahesil, area, status
- 🔍 **Filters** — search by name/village, filter by block, tahesil, and status
- 🛰 **Satellite / Map toggle** built-in
- 📊 **Live stats strip** — total farmers, villages, blocks, completed count
- 📦 **Marker clustering** — handles 1000+ pins smoothly

---

## 🚀 Deploy to GitHub Pages (free hosting)

### Step 1 — Ensure Google Sheet is public
1. Open your sheet: [Map_Details](https://docs.google.com/spreadsheets/d/1TUhunYkXjUaAzQuMmvF3DAquJVGjWmtPIshM2EvKkzw)
2. Click **Share** → **General access** → set to **"Anyone with the link"** → **Viewer**
3. Click **Done**

### Step 2 — Create a GitHub repository
1. Go to [github.com](https://github.com) → Sign in (or create free account)
2. Click the **+** button → **New repository**
3. Name it: `atamnirbhar-map` (or anything you like)
4. Set to **Public**
5. Click **Create repository**

### Step 3 — Upload the files
**Option A — GitHub website (easiest):**
1. In your new repo, click **Add file** → **Upload files**
2. Drag and drop `index.html` from this folder
3. Click **Commit changes**

**Option B — VS Code with Git:**
```bash
# In VS Code terminal, navigate to this folder:
cd path/to/atamnirbhar-map

# Initialize git and push:
git init
git add .
git commit -m "Initial farmer map"
git branch -M main
git remote add origin https://github.com/YOUR_USERNAME/atamnirbhar-map.git
git push -u origin main
```

### Step 4 — Enable GitHub Pages
1. In your repo, go to **Settings** (top tab)
2. Scroll to **Pages** in the left sidebar
3. Under **Source**, select **Deploy from a branch**
4. Set branch to **main**, folder to **/ (root)**
5. Click **Save**
6. Wait ~60 seconds, then your live URL appears:
   ```
   https://YOUR_USERNAME.github.io/atamnirbhar-map/
   ```

---

## 🗂 Project Structure

```
atamnirbhar-map/
└── index.html        ← entire app (single file, no build tools needed)
```

---

## 🔧 Customisation

### Update the Google Sheet ID
In `index.html`, find this section and replace the ID if you ever move the sheet:
```javascript
const SHEET_ID = '1TUhunYkXjUaAzQuMmvF3DAquJVGjWmtPIshM2EvKkzw';
const SHEET_GID_FARMERS = '1503472373';  // "Farmer details" tab
const SHEET_GID_MAPDATA = '866968192';   // Sheet2 (with lat/lng columns)
```

### Add more blocks/colours
Find `BLOCK_COLORS` and add more hex colours to the array.

### How coordinates work
- Farmers in **Sheet2** (survey tab) have exact `Latitude`/`Longitude` → plotted precisely
- Farmers in **Sheet1 only** (registry, ~1000 names) are placed near their village/block area with small random offsets so all pins are visible
- As you add more GPS data to Sheet2, those farmers will automatically get precise pins

---

## 📱 Works on
- Desktop browsers (Chrome, Firefox, Edge, Safari)
- Mobile browsers (responsive design)
- No installation, no server, no build step needed

---

## 🌱 Tech Stack
- [Leaflet.js](https://leafletjs.com/) — interactive maps
- [Leaflet.MarkerCluster](https://github.com/Leaflet/Leaflet.markercluster) — handles 1000+ pins
- [PapaParse](https://www.papaparse.com/) — reads CSV from Google Sheets
- [OpenStreetMap](https://openstreetmap.org/) + Esri Satellite — base tiles
- Google Fonts (Nunito + Playfair Display)

---

*Built for Atamnirbhar Society — Uttarkashi, Uttarakhand*
