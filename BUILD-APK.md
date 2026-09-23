# HDD Profile Studio — Install & Build to APK

The app is a single self-contained offline web app (a PWA). It needs **no internet** after the first load and stores nothing on any server. You have three ways to get it onto your phone, from easiest to "real APK".

---

## Option A — Install as an app (no build, works today) ✅ recommended first

This gives you a full-screen, offline app icon on your home screen in under a minute. It is the fastest path and is genuinely offline.

**On your Android phone (Chrome):**
1. Put the `HDD Profile App` folder online *once* so the phone can load it (any of these):
   - Host it free on **Netlify Drop** (drag the folder onto https://app.netlify.com/drop), **GitHub Pages**, or **Cloudflare Pages**; **or**
   - Serve it from your PC on the same Wi‑Fi (see "Run locally" below) and open your PC's IP from the phone.
2. Open the app URL in Chrome on the phone.
3. Tap the **⋮ menu → "Add to Home screen"** (or "Install app").
4. Open it from the new icon. Turn on Airplane mode — it still works. Done.

> A service worker caches everything on first open, so after step 3 it runs with no network at all.

---

## Option B — Wrap into a real .apk with PWABuilder (easiest true APK)

PWABuilder (by Microsoft) turns the PWA into a signed Android app package.

1. Host the folder online (Netlify Drop / GitHub Pages / Cloudflare Pages) so you have an `https://…` URL.
2. Go to **https://www.pwabuilder.com**, paste that URL, press **Start**.
3. Open the **Android** tile → **Download**. You get an `.apk` (and `.aab`).
4. Copy the `.apk` to your phone and install it (enable "Install unknown apps" for your file manager).

*Note:* PWABuilder's Android package is a "Trusted Web Activity" — it points at the hosted URL but still caches offline via the service worker. If you want an APK that contains the files inside it with **zero hosting**, use Option C.

---

## Option C — Bundled offline APK with Capacitor (files packed inside the APK)

Best if you want a standalone `.apk` that carries the app inside it and never needs a URL. Requires a one-time setup on your PC.

**Prerequisites (install once):**
- **Node.js LTS** — https://nodejs.org
- **Android Studio** — https://developer.android.com/studio (installs the Android SDK + JDK)

**Steps (run in a terminal):**
```bash
# 1. New Capacitor project
npm create @capacitor/app hdd-profile -- --name "HDD Profile Studio" --package-id in.trenchless.hddprofile
cd hdd-profile
npm install

# 2. Replace the starter web files with this app:
#    delete everything inside the "www" (or "dist") folder,
#    then copy the entire contents of "HDD Profile App" into it
#    (index.html must sit at the root of that folder).

# 3. Add Android and open it
npm install @capacitor/android
npx cap add android
npx cap copy
npx cap open android
```
5. In **Android Studio**: **Build → Build Bundle(s)/APK(s) → Build APK(s)**.
6. Find the file at `android/app/build/outputs/apk/debug/app-debug.apk`, copy to your phone, install.

To make a **signed release APK** (for sharing/Play Store): Android Studio → **Build → Generate Signed Bundle / APK**, create a keystore, follow the wizard.

---

## Run locally on your PC (for testing or Wi‑Fi install)

The app needs to be served over `http(s)`, not opened as a `file://` (service workers require it). Any static server works. Two zero-dependency options:

**Python (if installed):**
```bash
cd "HDD Profile App"
python -m http.server 8000
```
Then open `http://localhost:8000` on the PC, or `http://<your-PC-IP>:8000` on your phone (same Wi‑Fi).

**Node (if installed):**
```bash
cd "HDD Profile App"
npx serve .
```

---

## What's inside

```
HDD Profile App/
├── index.html            ← the whole app (UI + geometry engine), self-contained
├── manifest.webmanifest  ← app name, icons, standalone display
├── sw.js                 ← service worker → full offline caching
├── icons/                ← app icons (svg + png 192/512 + maskable)
└── BUILD-APK.md          ← this file
```

Everything is offline and local. No analytics, no network calls, no data leaves the device.
