# 🎉 Party Quest Photo Booth

A self-contained photo-booth web app for an iPad. Live camera preview, four game-adventure frames, a 3-2-1 countdown, one-tap capture, and an on-device gallery. Built to run full-screen and locked to a single app so party guests can't wander off into other apps.

---

## What's in this folder

```
index.html              the whole app (HTML + CSS + JS, no build step)
manifest.webmanifest    makes it installable / full-screen
icon-180/192/512*.png   home-screen + install icons
frames/frame1-4.svg     the four frames (reference / editable)
```

---

## Part 1 — Put it online (GitHub Pages)

The camera **only works over HTTPS**, which GitHub Pages gives you for free.

1. Create a new GitHub repo (e.g. `party-booth`).
2. Upload **all** the files in this folder, keeping the `frames/` folder and the icons next to `index.html`.
3. Repo → **Settings → Pages**.
4. Under "Build and deployment", Source = **Deploy from a branch**, Branch = **main**, folder = **/ (root)**. Save.
5. Wait ~1 minute. Your URL appears at the top: `https://YOURNAME.github.io/party-booth/`.

Open that URL on the iPad in **Safari** and tap **TAP TO START** — Safari will ask for camera permission. Tap **Allow**.

---

## Part 2 — Make the iPad a kiosk

A website can't lock the iPad by itself — these are quick one-time iOS settings.

### A. Launch it full-screen (no Safari bars)
1. In Safari, open your Pages URL.
2. Tap the **Share** button → **Add to Home Screen** → **Add**.
3. Close Safari and open the **Party Booth** icon from the Home Screen. It now runs full-screen like a real app.

### B. Keep the screen awake
**Settings → Display & Brightness → Auto-Lock → Never.**
(The app also requests a wake-lock automatically, but this is the reliable belt-and-suspenders setting.)

### C. Lock it to ONE app (guests can't switch apps) — Guided Access
1. **Settings → Accessibility → Guided Access → turn ON.**
2. Set **Passcode Settings → Set Guided Access Passcode** (pick something guests won't guess).
3. Open the **Party Booth** app from the Home Screen.
4. **Triple-click** the side/top button (or Home button on older iPads). Tap **Start**.
   - The iPad is now locked to this app. The Home gesture, app switcher, and notifications are disabled.
5. To exit later: triple-click again and enter your passcode.

That's the whole kiosk. Guests can only use the booth.

---

## Where the photos go

- **Every photo is saved automatically on the iPad** inside the app's gallery (browser IndexedDB). Tap the **picture icon** (top-right) to see them all. They survive reloads.
- To move them into the iPad's **Photos app**: open the gallery and tap **Save All to Photos** (or **Save to Photos** on a single one). iOS shows the share sheet — choose **Save Image(s)**. You can also AirDrop them to your phone/Mac from there.

> ⚠️ At the end of the party, do a **Save All to Photos** before doing anything else. The in-app gallery lives in Safari's storage — if someone later clears Safari/website data, those copies are gone. Saving to Photos (or AirDrop) makes a permanent copy.

---

## Customizing

- **Banner text** (default `KARY IS 6!`): tap the **gear icon** in the app, or change the default in `index.html` (search for `booth_title`). Max ~18 characters so it fits.
- **Frames**: the four designs live both inside `index.html` (the `FRAMES` array, which the app actually uses) and as editable copies in `frames/`. To change a frame, edit its SVG and paste the new markup into the matching entry of the `FRAMES` array.
- **Front vs. rear camera**: tap the flip icon next to the shutter.
- **Landscape or portrait**: tap the rotate icon (shows `4:3` / `3:4`) next to the shutter. Each frame has a dedicated landscape and portrait design — they're swapped, never stretched, so coins and text stay perfectly round and crisp. The saved photo matches whichever you chose.

---

## Good to know

- Works in Safari on iPadOS 16.4+ (needed for the wake-lock and multi-photo share). Camera + capture work on older versions too.
- The pixel font loads from Google Fonts; if the venue Wi-Fi is flaky, load the app once while online so it's cached. Photos still capture fine either way — only the title's pixel styling falls back to a plain font offline.
- No data leaves the iPad. There's no server; everything is local.
