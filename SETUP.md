# 🌿 Hedychium Farmer Map – Setup Guide

**Project:** Leaflet.js interactive map of Hedychium spicatum farmers  
**Org:** Aatmanirbhar Society, Uttarakhand  
**Stack:** HTML + Leaflet.js + Google Sheets API (no backend needed)

---

## What you'll build

A live webpage that:
- Pulls farmer data directly from your Google Sheet
- Shows every farmer as a pin on the map
- Clusters pins when zoomed out
- Shows name, village, area (nali), kg planted on click
- Has village filter + name search
- Displays live stats (total farmers, nali, kg)

---

## Step 1 – Prepare your Google Sheet

### 1a. Add GPS coordinates column
Your **Sheet2** already has a `GPS coordinates` column. For every farmer, add their lat/long like this:

```
30.922174, 78.391418
```

Use the GPS Map Camera app (like in your photos) to get coordinates in the field.

### 1b. Make the sheet Public
> ⚠️ Required – otherwise the map can't read the data

1. Open your Google Sheet
2. Click **Share** (top right)
3. Under "General access" → change to **"Anyone with the link"**
4. Set role to **Viewer**
5. Click **Done**

---

## Step 2 – Get your Sheet ID

Look at the URL of your Google Sheet:

```
https://docs.google.com/spreadsheets/d/  1BxiMVs0XRA5nFMdKvBdBZjgmUUqptlbs74OgVE2upms  /edit
                                          ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
                                          This is your SHEET_ID
```

Copy the long ID string between `/d/` and `/edit`.

---

## Step 3 – Edit index.html

Open `index.html` and find these two lines near the top of the `<script>` section:

```javascript
const SHEET_ID   = 'YOUR_GOOGLE_SHEET_ID';   // ← paste your ID here
const SHEET_NAME = 'Sheet2';                 // ← sheet tab name (check it matches)
```

Replace `YOUR_GOOGLE_SHEET_ID` with your actual Sheet ID.

**Example:**
```javascript
const SHEET_ID   = '1BxiMVs0XRA5nFMdKvBdBZjgmUUqptlbs74OgVE2upms';
const SHEET_NAME = 'Sheet2';
```

---

## Step 4 – Add more village coordinates (optional)

In `index.html`, find the `VILLAGE_COORDS` object and add entries for any villages in your data:

```javascript
const VILLAGE_COORDS = {
  'dangurgoan': [30.9222, 78.3914],
  'bariya':     [30.9268, 78.3905],
  'rana':       [30.9268, 78.3905],
  // Add your villages here:
  'hanuman chatti': [30.92XX, 78.39XX],
};
```

Farmers **without** a GPS coordinate in the sheet will be placed at their village centroid with a slight random offset so pins don't stack.

---

## Step 5 – Deploy to GitHub Pages (free hosting)

### 5a. Create a GitHub repo
1. Go to [github.com](https://github.com) → **New repository**
2. Name it `hedychium-map`
3. Set to **Public**
4. Click **Create repository**

### 5b. Upload your file
1. On the repo page, click **Add file → Upload files**
2. Drag `index.html` into the box
3. Click **Commit changes**

### 5c. Enable GitHub Pages
1. Go to **Settings → Pages** (left sidebar)
2. Under "Source" → select **Deploy from a branch**
3. Branch: **main** | Folder: **/ (root)**
4. Click **Save**
5. Wait ~1 minute, then your map is live at:
   ```
   https://YOUR-USERNAME.github.io/hedychium-map/
   ```

---

## Step 6 – Test it

1. Open the URL in your browser
2. You should see pins on the map around Uttarkashi / Barkot area
3. Click any pin to see farmer details
4. Use the Village dropdown and Search box to filter
5. Click **⟳ Refresh Data** to pull latest changes from the Sheet

---

## Column mapping (what the map reads from your Sheet)

| Sheet Column | Used For |
|---|---|
| Farmers Name | Pin label & search |
| Husband Name | Popup detail |
| Village | Filter dropdown & fallback location |
| Post office | Popup detail |
| Tehsil | Popup detail |
| Area under cultivation (nali) | Stats counter |
| Planting material distributed (Kg) | Stats counter |
| GPS coordinates | Exact pin location |
| Cropping System | Popup detail |

---

## Adding GPS coordinates in the field

Use the **GPS Map Camera** app (already on your phone – seen in your images).

After taking a photo, it stamps:
```
Lat 30.926803° Long 78.390542°
```

Enter these in your Sheet as: `30.926803, 78.390542`

---

## Troubleshooting

| Problem | Fix |
|---|---|
| Map shows "sample data" | Check SHEET_ID is correct & sheet is public |
| No pins visible | Check GPS column format: `30.92, 78.39` |
| Pins in wrong location | Check lat/lng aren't swapped (lat ~30, lng ~78 for Uttarakhand) |
| Data not updating | Click ⟳ Refresh, or hard-refresh browser (Ctrl+Shift+R) |

---

## File structure

```
hedychium-map/
└── index.html     ← everything in one file, no other files needed
```

---

*Built for Aatmanirbhar Society · Hedychium spicatum Partnership Farming 2026*
