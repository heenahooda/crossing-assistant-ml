# Smart Crossing Assistant: install on your phone

This folder is a PWA (Progressive Web App). Once it is hosted on HTTPS, you install it
from the browser and it opens like a normal app: its own icon, full screen, and it works offline.

Files:
- index.html          main app (dark, high-contrast version)
- warm.html           alternative warm/light version (open /warm.html to use it)
- manifest.webmanifest  app name, icons, colours
- sw.js               service worker (offline cache)
- icon-192.png, icon-512.png, icon-maskable-512.png

## Step 1: Put it online (free, about 5 minutes) with GitHub Pages
1. github.com -> New repository -> name it `crossing-assistant` -> Public -> Create.
2. "uploading an existing file" -> drag ALL the files from this folder (not the folder itself) -> Commit.
3. Settings -> Pages -> Source: "Deploy from a branch" -> Branch: main, folder: / (root) -> Save.
4. After about 1 minute your app is live at:
   https://heenahooda.github.io/crossing-assistant/
   (Quicker alternative: drag the folder onto https://app.netlify.com/drop)

Camera, microphone and installing only work on HTTPS, which both options give you.

## Step 2: Install on the phone
Android (Chrome, recommended):
  Open the link -> menu (three dots) -> "Install app" (or "Add to Home screen").
iPhone (Safari):
  Open the link -> Share button -> "Add to Home Screen".

## What works where
| Feature                         | Android Chrome | iPhone Safari |
|---------------------------------|:--------------:|:-------------:|
| Install as app + offline        | yes            | yes           |
| Camera preview                  | yes            | yes           |
| Spoken guidance (EN / 日本語)    | yes (needs a Japanese voice installed) | yes |
| Voice commands (start/stop/help)| yes            | limited / often not available |
| Vibration (haptic)              | yes            | no (Apple does not allow it in web apps) |

For the demo, use an Android phone with Chrome.
Allow Camera and Microphone when asked (first launch only).

## Updating the app later
Edit the files, upload them again, and change `crossing-assistant-v1` to `-v2` in sw.js
so phones pick up the new version.

## Optional: a real APK (Android installer file)
Easiest: go to https://www.pwabuilder.com, paste your hosted URL, choose Android, download the package.
Or with Capacitor (needs Node and Android Studio):
  npm init -y
  npm i @capacitor/core @capacitor/cli @capacitor/android
  npx cap init "Smart Crossing Assistant" com.heena.crossing --web-dir=.
  npx cap add android
  npx cap sync
  npx cap open android      (then Build -> Build APK in Android Studio)
Add CAMERA, RECORD_AUDIO and VIBRATE permissions in AndroidManifest.xml.
Note: the browser speech-recognition API is not guaranteed inside a Capacitor WebView,
so for voice commands in an APK you would add a speech-recognition plugin. The hosted PWA
in Chrome needs no extra work.
