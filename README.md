# androidClone

A tiny “android UI in the browser” prototype. This repo currently ships as a single-page `index.html` that lays out common Android-style UI copy (lock screen time/date, “Swipe up to unlock”, quick settings toggles, and a notification-style message) for a lightweight visual clone / mock. :contentReference[oaicite:0]{index=0}


---

## What it is

- A minimal web mock of Android-style screens/components (lockscreen + quick settings style labels/toggles + notification text). :contentReference[oaicite:2]{index=2}
- No build tooling, no dependencies (open the HTML directly or serve it locally). :contentReference[oaicite:3]{index=3}

## Current UI text included

From the current `index.html` content:

- Lockscreen-style time/date + “Swipe up to unlock”
- Status/weather line (e.g., “Mon, Jan 1 • 22°C”)
- Search bar label
- Quick toggles: Wi-Fi, Bluetooth, Dark Theme, Airplane
- Notification-style message: “System Update • Now … All Apps Activated …” :contentReference[oaicite:4]{index=4}

## Project structure

```text
andoridClone/
├─ index.html
├─ LICENSE
├─ CODE_OF_CONDUCT.md
└─ SECURITY.md
