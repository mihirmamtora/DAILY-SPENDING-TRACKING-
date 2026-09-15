# Mera Hisaab — Play Store Publishing Guide

This folder is a real installable web app (PWA), not just a chat artifact. Here's exactly how to turn it into a Play Store listing.

## Step 1 — Put it online (needs a real URL)
Play Store packaging tools need to fetch your app from a live URL — they can't wrap local files.

You've done this before with GitHub Pages, so the fastest path:
1. Create a new GitHub repo (e.g. `mera-hisaab`).
2. Upload all 5 files from this folder: `index.html`, `manifest.json`, `service-worker.js`, `icon-192.png`, `icon-512.png` (and `icon-512-maskable.png`).
3. Settings → Pages → deploy from the `main` branch, root folder.
4. Your app is now live at `https://<yourusername>.github.io/mera-hisaab/`.
5. Open that URL on your phone — you should see "Add to Home screen" / "Install app" appear. That confirms the PWA is working.

## Step 2 — Wrap it into an Android app (.aab file)
Play Store requires an **Android App Bundle (.aab)**, signed with a key. The free, no-code way to generate this from a PWA:

1. Go to **pwabuilder.com**
2. Paste your GitHub Pages URL and click "Start"
3. It scans your manifest and service worker (already included and configured)
4. Click "Package for Stores" → choose **Android**
5. It generates a signed `.aab` file plus a signing key — **download and save this key safely**, you'll need it for every future update

## Step 3 — Google Play Console setup
1. Go to **play.google.com/console** → pay the one-time **$25 registration fee**
2. Create a new app → fill in name, category (Finance), description
3. Upload the `.aab` from Step 2
4. You'll need to provide, before it can go live:
   - **Privacy policy URL** (required even for local-only storage — a simple one-page statement saying "no data leaves your device" is enough; I can draft this for you)
   - App screenshots (phone size) — you can screenshot the app running in your browser
   - Feature graphic (1024×500 image) — I can design one
   - Content rating questionnaire
   - Data safety form — since this app stores everything locally and sends nothing anywhere, you'll answer "No data collected"
5. Submit for review — Google typically takes a few hours to a few days for a first-time review

## Notes
- All transaction data stays in the phone's local storage — nothing is uploaded anywhere, which also simplifies the Data Safety form.
- Every time you update the app, you re-run Step 2 (PWABuilder) with the same signing key and upload the new `.aab` as a new version in Play Console.
