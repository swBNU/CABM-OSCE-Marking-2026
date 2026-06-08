# OSCE Marker — offline PWA

A self-contained web app for OSCE stations: marking grid, examination sounds,
a station timer with an audible bell, and one-tap export of all marks to Excel.
No App Store, no backend, no running costs.

## What's in here
- `index.html` — the whole app (edit your stations & checklists at the top)
- `xlsx.full.min.js` — Excel export library (bundled, works offline)
- `manifest.webmanifest`, `service-worker.js`, `icons/` — makes it installable & offline
- `sounds/` — drop your own audio files here

## 1. Customise your stations
Open `index.html`. Near the top of the `<script>` block you'll find a `STATIONS`
array and a `SOUNDS` array. Edit the station names, checklist items, marks-per-item
(`max`), timer minutes, and sound files. That's the only part you need to touch.

## 2. Host it free on GitHub Pages
1. Create a free GitHub account and a new **public** repository (e.g. `osce-marker`).
2. Upload every file in this folder (keep the folder structure — `icons/` and `sounds/`).
3. Repo **Settings → Pages → Build and deployment → Source: Deploy from a branch**,
   pick `main` / root, Save.
4. After a minute you'll get a URL like `https://yourname.github.io/osce-marker/`.

(Cloudflare Pages or Netlify free tier work the same way if you prefer.)

## 3. Install on each iPad
1. Open the URL in **Safari** on the iPad (do this once with wifi so it caches).
2. Tap the **Share** icon → **Add to Home Screen**.
3. It now opens full-screen like an app and works offline.
Repeat on all 5–6 iPads.

## 4. On exam day
- Pick the station, enter candidate number + examiner, tick the grid, set a global rating.
- **Save mark** stores it on that iPad (kept even if Safari closes or wifi drops).
- At the end, tap **Export** → an `.xlsx` is downloaded with a Summary sheet plus
  one sheet per station. AirDrop / email / upload those files and combine them.

## How marking works
- Each station scores the five learning outcomes **LO1–LO5** as a number out of
  `LO_MAX` (default 100). The **average** of the five is shown live as a percentage.
- **Overall status** is calculated automatically from that average:
  `<45% Fail` · `45–49% VIVA` · `≥50% Pass`
  (the average is rounded to the nearest whole percent for banding).
- Two manual viva buttons let the examiner record the post-viva result, overriding the
  auto status: **Passed VIVA – 50%** (capped pass) and **Failed VIVA**, which records
  **Failed VIVA – <their %>** using the candidate's actual average. The two are mutually exclusive.
- **Attempt = "Viva – capped 50"** caps the average at 50% before the status is worked out.
- **Any red flag failures = Yes** overrides the status to **Fail – red flag**, whatever the score.

## Sounds included (add the audio files to /sounds)
`normal-vesicular.mp3`, `fine-crackles.mp3`, `wheeze.mp3`, `s1-s2.mp3`, `s3.mp3`, `pericardial-rub.mp3`
(any of `.mp3 / .m4a / .wav` work — just match the filename in the `SOUNDS` list).

## Timer
- Presets are **10 min** and **15 min**, plus a **+25% extra time** button for
  access-arrangement candidates (adds a quarter of the selected time).

## Notes
- Marks are stored locally per iPad (`localStorage`). Export before wiping a device.
- The timer's bell uses the device's audio — tap Start once so iOS allows sound.
