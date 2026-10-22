# Crossing Assistant (redesign): put this in the `crossing-assistant-ml` repo only

Leave your existing `crossing-assistant` repository untouched. Upload these files to
`crossing-assistant-ml` (replace its index.html / warm.html / sw.js / manifest / icons).

Files
- index.html   dark, high-contrast theme (main app)
- warm.html    warm/light theme, same structure and behaviour
- manifest.webmanifest, sw.js, icon-*.png   installable-app files (PWA)

## Install (same as before)
1. Upload all files (not the folder) to the repo, then Settings -> Pages -> Deploy from branch -> main / root.
2. Android Chrome: open the link -> menu -> Install app. iPhone Safari: Share -> Add to Home Screen.
3. After uploading a new version, change `crossing-assistant-ml-v1` to `-v2` in sw.js so phones update.

## What changed (your 6 points)
1. Navigation: the four tabs are gone. Home = one big control. Settings, Help & Instructions,
   Research testing and About are separate screens, each with a Back button.
2. Main action: one large START ASSISTANCE button that turns into STOP ASSISTANCE and announces the
   state aloud.
3. Microphone: no more "tap to listen". Home shows a Status list: Audio guidance, Voice commands,
   Vibration feedback, Camera, Detection. "Listening" appears only after the browser confirms the mic
   is really listening; otherwise it says Off / Unavailable on this device / permission needed.
4. Emergency / Help: lives on the Help screen. It says clearly that the prototype cannot contact anyone,
   lists 110 (police) and 119 (fire/ambulance) for Japan, and the practice button is labelled demo only.
5. The process diagram moved to About this project. VR test moved to Research & testing.
6. Accessibility: headings and landmarks, focus moves to each screen's heading, labelled switches,
   skip link, live regions for screen readers, 44-56 px+ targets, visible focus ring, reduced-motion
   support, no information by colour alone, failures are spoken and shown (camera, audio, mic).
   Spoken guidance can be switched off in Settings so TalkBack/VoiceOver users do not hear everything twice.

Safety wording: the app never says "safe to cross" or "you may cross". Green now says
"Green pedestrian signal detected. Check for traffic before you cross." and the home screen always shows
"Research prototype · Not validated for independent road crossing".

## About the .tflite model (important)
The app does NOT run your .tflite yet, and says so: Detection shows "Simulated (no model loaded)".
Putting the file in the repo does not make the camera use it. To wire it up the app must load the model with a
TFLite/TensorFlow.js runtime, convert each camera frame to the model's input size and format, run it, and
decode the output tensors into crosswalk / signal state / distance. For that I need: the .tflite file (or its
input and output shapes), the class names, the input size and normalisation, and any confidence threshold.

## Browser support
Android Chrome: everything. iPhone Safari: install, camera and speech output work; vibration is blocked by Apple
and voice commands are limited, and the Status list will say so honestly.
