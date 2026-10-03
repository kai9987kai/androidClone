# NovaDroid Web OS 2026 Ultra

A highly interactive browser-based mobile operating system simulation built entirely with HTML, CSS, and JavaScript.

NovaDroid started as an Android-inspired web interface and has evolved into a much more complete browser-based operating environment featuring persistent applications, gesture navigation, an app back stack, Recents, IndexedDB photo storage, dynamic theming, diagnostics, a terminal, local files, notifications, accessibility features, hardware API integration, and a self-testing system.

The entire operating system runs from a **single HTML file**.

---

## Overview

NovaDroid Web OS is an experimental project exploring how far a modern web browser can be pushed toward behaving like a lightweight operating system.

Rather than simply recreating the appearance of Android, NovaDroid implements many operating-system-style concepts internally:

- Application lifecycle management
- App switching
- Application history
- Gesture navigation
- Persistent state
- Binary photo storage
- Notifications
- Quick settings
- Hardware capability detection
- Runtime diagnostics
- Application cleanup
- Keyboard navigation
- Local file handling
- A simulated command shell
- Backup and restore
- Accessibility controls
- Browser API abstraction

The project requires no framework, build system, server-side runtime, package manager, or external database.

Open the HTML file and NovaDroid boots.

---

# Features

## Operating System Interface

NovaDroid includes a complete mobile-style interface with:

- Lock screen
- Home screen
- Status bar
- App launcher
- Searchable app drawer
- Notification shade
- Quick Settings
- Navigation gesture area
- Recent Apps
- Dynamic wallpapers
- Light mode
- Dark mode
- Dynamic accent colours
- Brightness controls
- Volume controls
- Fullscreen mode
- Toast notifications
- Dialog system
- Command palette

---

# Navigation System

NovaDroid has a substantially more advanced navigation model than the original prototype.

## Home

Tap the bottom navigation gesture area to immediately return to the Home screen.

## Swipe Home

While inside an application, swipe upward from the bottom navigation area to return Home.

## App Drawer

Swipe upward while already on the Home screen to open the application drawer.

## Recent Apps

Press and hold the bottom gesture area to open Recent Apps.

## Back

Use the left-edge predictive-style gesture or supported keyboard controls to travel backwards through application history.

NovaDroid maintains an actual application stack rather than simply closing every application and returning Home.

For example:

```text
Home
  ↓
Settings
  ↓
Device Lab

Back

Device Lab
  ↓
Settings
```

## Keyboard Navigation

Supported shortcuts include:

```text
Ctrl + K       Open command palette
Alt + Left     Back
Escape         Close modal / Back
Home           Return Home where supported
```

---

# Applications

NovaDroid currently contains **16 built-in applications**.

## Messages

A local simulated messaging application.

Features:

- Conversation list
- Message history
- Send messages
- Simulated replies
- Persistent conversation state
- Message previews

---

## Camera

Uses the browser MediaDevices API where supported.

Features:

- Live camera preview
- Front/rear camera switching
- Photo capture
- JPEG generation
- Flash animation
- Camera thumbnail
- Automatic stream cleanup
- Race-condition protection
- IndexedDB photo storage

Camera resources are automatically released whenever the user leaves the Camera application.

This prevents abandoned `MediaStreamTrack` objects from continuing to use the webcam.

---

## Photos

A persistent photo gallery connected to NovaDroid's photo database.

Features:

- IndexedDB-backed storage
- Thumbnail grid
- Full image viewer
- Delete photos
- Export photos
- Object URL lifecycle management
- Memory-storage fallback

NovaDroid revokes unused Blob URLs when appropriate to reduce memory leaks.

---

## Web

A sandboxed browser interface.

Features:

- Address bar
- URL validation
- Navigation history
- Back
- Forward
- Home
- Sandboxed iframe rendering
- Search handling
- External-browser fallback
- Online/offline awareness

Some external websites prevent iframe embedding using browser security headers. NovaDroid detects and works around these limitations where possible.

---

## Calculator

A functional calculator with a dedicated arithmetic parser.

Supported operations include:

```text
+
-
*
/
()
decimals
```

Unlike the original prototype, mathematical expressions are parsed instead of being executed as JavaScript.

---

## Clock

Includes:

- Live digital clock
- Analogue clock
- Stopwatch
- Countdown timer
- Persistent timer architecture
- Background-safe timer state

---

## Notes

Persistent note-taking application.

Features:

- Create notes
- Edit notes
- Delete notes
- Persistent storage
- Multi-line content
- Automatic UI refresh

---

## Calendar

Interactive monthly calendar.

Features:

- Current-day highlighting
- Month navigation
- Event creation
- Persistent events
- Date selection

---

## Maps

Embedded OpenStreetMap-based mapping interface.

Features:

- Interactive maps
- Search interface
- Dark-mode adaptation
- Embedded map rendering

---

## Mail

Local mail simulation.

Features:

- Inbox
- Read/unread state
- Message viewer
- Local mail composition
- Persistent message data

No real email is transmitted.

---

## Tasks

Persistent task-management application.

Features:

- Create tasks
- Complete tasks
- Delete tasks
- Persistent state
- Simple productivity workflow

---

## Files

Local file inspection interface.

Files remain on the user's computer unless explicitly processed by browser functionality.

Features:

- Local file selection
- File metadata
- Local file handling
- Object URL management
- No automatic upload

---

## Terminal

NovaDroid includes its own simulated command environment.

Example:

```text
nova$ help
nova$ apps
nova$ open camera
nova$ open settings
nova$ theme
nova$ date
nova$ online
nova$ storage
nova$ echo Hello NovaDroid
nova$ clear
```

The Terminal does **not** execute host operating-system shell commands.

It communicates only with NovaDroid's internal environment.

---

## Device Lab

Device Lab provides information about the browser and hardware environment running NovaDroid.

Depending on browser support it can inspect:

- Browser capabilities
- CPU logical thread count
- Device memory hints
- Viewport resolution
- Battery information
- Network state
- Storage estimates
- IndexedDB support
- MediaDevices support
- Vibration support
- Clipboard support
- Web Share support
- Wake Lock support
- Fullscreen support
- File System Access support

Device Lab also acts as NovaDroid's built-in diagnostics environment.

---

## Phone

A simulated phone dialler.

Features:

- Numeric keypad
- Call simulation
- Recent-call state

NovaDroid does not initiate real telephone calls automatically.

---

## Settings

The Settings application provides centralised control of the NovaDroid environment.

### Connectivity

- Wi-Fi
- Bluetooth
- Airplane mode
- Do Not Disturb

### Appearance

- Light mode
- Dark mode
- Dynamic accent colour
- Wallpaper selection
- Brightness

### Audio

- Volume controls

### Accessibility

- Reduce Motion
- Optional haptic feedback

### Power

- Screen Wake Lock where browser support exists

### System

- Fullscreen
- Device information
- Storage information
- Diagnostics
- Backup
- Restore
- Reset NovaDroid

---

# Quick Settings

The notification shade includes interactive system controls.

Current controls include:

```text
Wi-Fi
Bluetooth
Dark Theme
Airplane Mode
Do Not Disturb
Brightness
Volume
```

Quick Settings are connected to the same central state system used by the Settings application.

---

# Persistent State

NovaDroid persists supported operating-system state using browser storage.

Examples include:

```text
Theme
Accent colour
Wallpaper
Brightness
Volume
Wi-Fi state
Bluetooth state
Airplane mode
Do Not Disturb
Notes
Messages
Tasks
Calendar events
Mail
Calls
Notifications
Recent applications
Accessibility preferences
Power preferences
```

Refreshing the browser therefore does not normally reset the operating system.

---

# State Validation and Recovery

Persistent data is treated as potentially untrusted or corrupt.

NovaDroid validates restored state before using it.

The system can recover from:

- Invalid JSON
- Invalid arrays
- Unsupported application IDs
- Invalid brightness values
- Invalid volume values
- Invalid accent colours
- Invalid wallpaper indexes
- Missing state fields
- Older state schemas

The current persistence system uses a state schema so future NovaDroid versions can support migration between versions.

---

# Photo Database

Photos are stored separately from the primary NovaDroid state.

Architecture:

```text
Camera
   │
   ▼
Canvas
   │
   ▼
JPEG Blob
   │
   ▼
IndexedDB
   │
   ▼
Photos
```

This avoids storing large Base64 images directly inside normal application state.

If IndexedDB is unavailable, NovaDroid can fall back to temporary session memory.

---

# Application Lifecycle

NovaDroid manages application lifecycle events centrally.

Conceptually:

```text
openApp()
   │
   ├── clean previous application resources
   │
   ├── update app history
   │
   ├── mount application UI
   │
   ├── initialise application
   │
   └── update system UI
```

When leaving an application:

```text
cleanupApp()
   │
   ├── stop camera streams
   ├── revoke temporary object URLs
   ├── stop application-specific resources
   └── release temporary state
```

This significantly reduces resource leaks.

---

# Camera Resource Safety

Camera handling contains additional race-condition protection.

Consider this sequence:

```text
1. Camera requests webcam access
2. User immediately leaves Camera
3. Browser finishes permission request
4. Media stream becomes available
```

A naive implementation could attach that stream even though Camera is no longer open.

NovaDroid checks whether Camera is still active before attaching the stream.

If not, the newly created stream is immediately stopped.

---

# Application Back Stack

NovaDroid maintains application history internally.

Example:

```text
Home
  ↓
Settings
  ↓
Device Lab
  ↓
Files
```

Repeated Back actions produce:

```text
Files
  ↓
Device Lab
  ↓
Settings
  ↓
Home
```

This produces much more realistic mobile navigation than always closing the current application.

---

# Recents

NovaDroid includes a Recent Apps system.

Recent applications are tracked as applications are opened and can be accessed through the navigation gesture area.

The Recents system is separate from Home navigation.

---

# Gesture Engine

Pointer events are used to distinguish between:

```text
Tap
Hold
Vertical swipe
Edge swipe
```

The bottom navigation area no longer uses the browser's `ns-resize` cursor.

This prevents the misleading up/down-arrow mouse icon that appeared in earlier versions.

Current behaviour:

```text
Tap bottom pill
→ Home

Swipe upward inside application
→ Home

Swipe upward on Home
→ App Drawer

Hold bottom pill
→ Recents

Edge swipe
→ Back
```

---

# Command Palette

Press:

```text
Ctrl + K
```

to open NovaDroid's global command palette.

The command system provides a foundation for future natural-language and system-level actions.

Future commands could include:

```text
Open Camera

Turn Wi-Fi off

Create note

Search files

Enable dark mode

Run diagnostics
```

---

# Backup and Restore

NovaDroid can export operating-system state to a backup file.

The backup can later be imported to restore supported system data.

Backup data can include:

```text
Preferences
Notes
Messages
Tasks
Events
Mail
Notifications
Calls
System settings
```

Binary photographs are managed independently through the photo database architecture.

---

# Diagnostics

NovaDroid includes built-in automated integrity tests.

Tests include:

- Application registry integrity
- Missing renderer detection
- Duplicate application detection
- Duplicate DOM ID detection
- localStorage accessibility
- IndexedDB availability
- Blob support
- Object URL support
- Camera stream cleanup
- Persistent-state integrity

Runtime problems can therefore be surfaced from within NovaDroid itself.

---

# Runtime Error Monitoring

NovaDroid monitors browser-level application errors using handlers such as:

```javascript
window.onerror
```

and:

```javascript
unhandledrejection
```

Captured errors can be exposed through Device Lab for debugging.

---

# Debug Interface

Development builds expose a read-only diagnostic interface:

```javascript
window.__novaDebug
```

It can provide controlled access to diagnostic information such as:

```text
Current OS state
Application stack
Current application
Camera status
Runtime errors
Self-test results
```

This is useful when developing new NovaDroid applications or debugging application lifecycle problems.

---

# Browser APIs

NovaDroid can use a number of modern browser APIs when available.

These include:

```text
MediaDevices API
IndexedDB
Web Storage
Battery Status API
Storage Manager API
Screen Wake Lock API
Fullscreen API
Clipboard API
Web Share API
Vibration API
File APIs
Hardware Concurrency
Device Memory hints
Navigator online state
Pointer Events
```

Feature detection is used so unsupported APIs do not prevent NovaDroid from booting.

---

# Graceful Degradation

NovaDroid is designed so optional browser APIs enhance the operating system rather than becoming mandatory dependencies.

For example:

```text
IndexedDB unavailable
        │
        ▼
Temporary photo storage
```

```text
Wake Lock unavailable
        │
        ▼
Setting marked unsupported
```

```text
Camera unavailable
        │
        ▼
Camera error state
```

This allows NovaDroid to run across a wider range of desktop and mobile browsers.

---

# Security

NovaDroid includes several protections appropriate for a browser-based operating environment.

These include:

- HTML escaping for user-generated content
- URL validation
- Sandboxed browser iframe
- Restricted external protocols
- State normalisation
- Prototype-pollution protection
- No host shell execution
- Local-only terminal
- Explicit browser permission requirements
- Local file isolation
- Media-stream cleanup

NovaDroid should still be treated as an experimental web application rather than a security boundary.

---

# Accessibility

NovaDroid includes several accessibility improvements.

Features include:

- Keyboard navigation
- Focus restoration
- Modal focus trapping
- Escape-key handling
- Reduced-motion support
- Accessible labels
- Larger interaction targets
- Dynamic status-bar contrast
- Optional haptic feedback
- Keyboard Back navigation

---

# Responsive Design

NovaDroid is designed around a smartphone form factor but scales to different viewport sizes.

The simulated device automatically adjusts where necessary to remain usable on smaller displays.

---

# Architecture

At a high level:

```text
┌───────────────────────────────────────────────┐
│                NOVADROID UI                   │
├───────────────────────────────────────────────┤
│ Lock Screen │ Home │ Drawer │ Shade │ Recents│
├───────────────────────────────────────────────┤
│              Application Engine               │
├───────────────────────────────────────────────┤
│   App Registry │ App Stack │ Lifecycle Hooks  │
├───────────────────────────────────────────────┤
│                 System APIs                   │
├───────────────────────────────────────────────┤
│ Persistence │ Photos │ Notifications │ Theme  │
├───────────────────────────────────────────────┤
│              Browser API Layer                │
├───────────────────────────────────────────────┤
│ IndexedDB │ MediaDevices │ Storage │ WakeLock │
├───────────────────────────────────────────────┤
│                Web Browser                    │
└───────────────────────────────────────────────┘
```

---

# Project Structure

NovaDroid currently follows a deliberately portable single-file architecture.

```text
novadroid_web_os_2026_ultra_homefix.html
```

Inside the HTML file are:

```text
HTML
├── Device shell
├── Lock screen
├── Home screen
├── Notification system
├── App drawer
├── Navigation system
└── Application container

CSS
├── Theme variables
├── Device layout
├── Material-inspired surfaces
├── Animation system
├── Dark theme
├── Responsive scaling
└── Accessibility rules

JavaScript
├── State manager
├── Persistence system
├── Application registry
├── Application lifecycle manager
├── Navigation stack
├── Gesture engine
├── Notification manager
├── Photo database
├── Backup manager
├── Diagnostics
└── Individual applications
```

---

# Installation

No installation process is required.

Download:

```text
novadroid_web_os_2026_ultra_homefix.html
```

and open it in a modern web browser.

For the best support for browser APIs, serving the file through `localhost` or HTTPS is recommended.

For example using Python:

```bash
python -m http.server 8000
```

Then open:

```text
http://localhost:8000/novadroid_web_os_2026_ultra_homefix.html
```

---

# Browser Requirements

A current Chromium-based browser is recommended.

Examples include:

- Google Chrome
- Microsoft Edge
- Chromium
- Brave

Firefox and Safari should support much of NovaDroid but some optional browser APIs may behave differently or be unavailable.

---

# Camera Requirements

Camera functionality normally requires a secure browser context.

Use either:

```text
https://
```

or:

```text
http://localhost
```

The browser will request camera permission when Camera is opened.

NovaDroid cannot bypass browser permission controls.

---

# Running Locally

Clone or download the project.

Then:

```bash
cd novadroid
python -m http.server 8000
```

Open:

```text
http://localhost:8000/
```

No npm installation is necessary.

There is no compilation process.

There are no production dependencies required to boot NovaDroid.

---

# Development

Because NovaDroid currently uses a single-file architecture, development can be performed directly in the HTML file.

Recommended development workflow:

```text
Edit HTML
   ↓
Reload browser
   ↓
Open Device Lab
   ↓
Run diagnostics
   ↓
Check browser console
   ↓
Test navigation
```

When modifying applications, verify:

```text
Application opens
Application closes
Back works
Home works
Recents works
State persists
Resources are cleaned
No duplicate DOM IDs exist
No runtime errors appear
```

Camera-related changes should additionally verify that all MediaStream tracks stop after leaving Camera.

---

# Testing

NovaDroid has been tested using automated Chromium smoke testing.

The test workflow includes:

```text
Boot NovaDroid
        ↓
Unlock
        ↓
Open every registered application
        ↓
Exercise Back
        ↓
Exercise Home
        ↓
Exercise Recents
        ↓
Inspect runtime errors
        ↓
Inspect console errors
        ↓
Validate DOM
```

A previous full application pass successfully opened all **16 applications** without uncaught JavaScript errors.

---

# Original Prototype vs NovaDroid Ultra

NovaDroid began as an Android web clone.

The current architecture goes considerably further.

| Capability | Original | NovaDroid Ultra |
|---|---|---|
| Applications | 12 | 16 |
| Persistent state | No | Yes |
| IndexedDB | No | Yes |
| Real Recents | No | Yes |
| App back stack | No | Yes |
| Gesture engine | Basic | Advanced |
| Predictive-style Back | No | Yes |
| Command palette | No | Yes |
| Tasks | No | Yes |
| Terminal | No | Yes |
| Device diagnostics | No | Yes |
| Backup/restore | No | Yes |
| Runtime error capture | No | Yes |
| State recovery | No | Yes |
| Front/rear camera | No | Yes |
| Browser history | No | Yes |
| Wake Lock | No | Yes |
| Reduced motion | No | Yes |
| Dynamic accent | No | Yes |
| Multiple wallpapers | No | Yes |
| Resource lifecycle manager | Limited | Yes |
| Self diagnostics | No | Yes |

---

# Why NovaDroid Is Different

NovaDroid is not intended to simply copy Android visually.

The long-term goal is to investigate whether browser technologies can form the foundation of a small self-contained operating environment.

The project combines ideas from:

- Mobile operating systems
- Progressive Web Apps
- Desktop environments
- Browser sandboxes
- Application runtimes
- Virtual filesystems
- Web hardware APIs
- Local-first software
- OS-level command systems

---

# Current Limitations

NovaDroid remains a browser application.

Therefore it cannot directly provide unrestricted access to:

- Host operating-system processes
- Native system settings
- Arbitrary filesystem locations
- Real SMS databases
- Real phone calls
- Installed Android applications
- Native Bluetooth device management
- Native Wi-Fi network management
- Root permissions
- Kernel functionality

Some features are simulations of OS behaviour rather than replacements for the host operating system.

External websites may also block iframe embedding.

Browser API support differs by browser and operating system.

---

# Roadmap

The next major architecture could transform NovaDroid from a collection of built-in apps into an extensible web operating environment.

## NovaDroid App SDK

Applications could register through a formal API:

```javascript
Nova.apps.register({
    id: "example",
    name: "Example",
    icon: "...",
    permissions: [],
    render() {},
    init() {},
    cleanup() {}
});
```

---

## Application Packages

Future NovaDroid versions could support installable packages such as:

```text
.nova
```

A package could contain:

```text
manifest.json
app.js
app.css
assets/
```

---

## Virtual Filesystem

Potential structure:

```text
/
├── system/
├── apps/
├── home/
│   ├── Documents/
│   ├── Pictures/
│   ├── Downloads/
│   └── Desktop/
├── temp/
└── config/
```

IndexedDB could provide persistent virtual filesystem storage.

---

## Permission Manager

Potential application permissions:

```text
camera
microphone
photos
files
notifications
clipboard
location
network
wake-lock
```

Each application would explicitly request capabilities.

---

## Process Manager

Future Device Lab versions could become a system task manager showing:

```text
Application
State
Memory estimate
Runtime
Permissions
Background status
```

---

## Widget Framework

Home-screen widgets could become installable components.

Examples:

```text
Weather
Clock
Calendar
Tasks
System Monitor
Battery
Notes
Music
```

---

## Notification API

Applications could receive a system-level API such as:

```javascript
Nova.notifications.push({
    app: "tasks",
    title: "Task due",
    body: "Finish NovaDroid README"
});
```

---

## Background Services

Future versions could implement controlled simulated services:

```text
Timer service
Notification scheduler
Sync service
Download manager
Media service
```

---

## Internal App Store

An experimental Nova Store could allow `.nova` packages to be installed into the virtual filesystem.

---

## Windowed Desktop Mode

Large displays could optionally transform NovaDroid into a desktop environment with:

- Resizable windows
- Multiple simultaneous applications
- Desktop icons
- Taskbar
- Snap layouts
- Keyboard multitasking

---

## Progressive Web App

NovaDroid could ultimately become installable using:

```text
manifest.webmanifest
service-worker.js
```

This would provide:

- Offline boot
- Home-screen installation
- Standalone display mode
- Cached system assets
- Faster startup

---

# Long-Term Vision

The long-term idea is:

```text
Browser
   │
   ▼
Nova Runtime
   │
   ├── App SDK
   ├── Package Manager
   ├── Virtual Filesystem
   ├── Permission Manager
   ├── Process Manager
   ├── Notification Service
   ├── Hardware API Layer
   └── Window Manager
            │
            ▼
       Nova Applications
```

At that point NovaDroid would no longer simply be an Android-style web simulation.

It would become a small experimental **browser-native operating environment**.

---

# Contributing

Contributions are welcome.

Useful contribution areas include:

- New applications
- Application SDK development
- Performance improvements
- Accessibility
- Gesture recognition
- Browser compatibility
- Virtual filesystem development
- IndexedDB improvements
- PWA support
- New widgets
- Permission management
- UI animations
- Automated testing
- Device Lab diagnostics
- Security improvements

When contributing, avoid introducing hard external dependencies unless they provide a substantial benefit.

The project's ability to run as a self-contained web application is one of its core characteristics.

---

# Design Principles

NovaDroid development follows several principles:

### Local First

User-created information should remain local whenever possible.

### Graceful Degradation

Missing browser APIs should disable individual capabilities rather than crash the operating system.

### Resource Safety

Applications should release cameras, timers, Blob URLs, event listeners, and other resources when they are no longer required.

### Persistent by Default

Useful application state should survive refreshes.

### Accessible

Keyboard navigation, reduced motion, appropriate focus management, readable contrast, and semantic interfaces should be considered core functionality.

### Portable

NovaDroid should remain easy to run and distribute.

### Experimental

The project should continue testing ideas that go beyond merely reproducing an existing mobile interface.

---

# Privacy

NovaDroid is designed primarily as a local browser application.

Data such as notes, tasks, messages, settings, and photos is stored using browser-local storage technologies unless an external feature is explicitly used.

Local files selected through the Files application are not automatically uploaded anywhere.

Camera access requires explicit browser permission.

---

# Disclaimer

NovaDroid Web OS is an experimental browser-based operating-system simulation.

It is not Android, is not affiliated with Google, and should not be treated as a replacement for the security or isolation mechanisms of a native operating system.

Android, Material Design, Chrome, and other referenced product names belong to their respective owners.

---

# Project Status

**Status:** Active Development

**Generation:** NovaDroid Web OS 2026 Ultra

**Architecture:** Single-file web operating environment

**Core technologies:**

```text
HTML5
CSS3
Vanilla JavaScript
IndexedDB
Web Storage
MediaDevices
Pointer Events
Modern Web APIs
```

---

# Final Goal

NovaDroid asks a simple question:

> **How close can a completely browser-native application get to behaving like its own operating environment?**

Each release pushes that experiment further.
