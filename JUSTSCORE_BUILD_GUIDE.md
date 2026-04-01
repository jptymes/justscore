# JustScore — File Map, Dependencies & Build Guide

**Product:** JustScore Basketball Scoreboard  
**Company:** JustInTymeSports, LLC  
**Live URL:** https://justscore.justintymesports.net  
**Hosting:** Netlify (GitHub → auto-deploy)  
**Last updated:** April 1, 2026  
**Current version:** v4.15  

---

## Purpose of This Document

This document is the single reference for:
- What every file does
- Which files reference which other files
- What must be updated when a version changes
- How to build and deploy a new version correctly

Drop this document into any new Claude session alongside CHANGELOG.md to restore full build context.

---

## Deployment Package — 25 Files

```
index.html                  ← Main scoreboard app (PRIMARY — changes most often)
manifest.json               ← PWA install config
sw.js                       ← Service worker / offline cache
favicon.ico                 ← Browser tab icon
_redirects                  ← Netlify HTTP→HTTPS and old URL redirects
CHANGELOG.md                ← Full project history and strategic context
JUSTSCORE_BUILD_GUIDE.md    ← This file — build and deploy reference
help.html                   ← Help page (justscore.justintymesports.net/help)
releases.html               ← Release notes page (/releases.html)
justscore-cheatsheet.html   ← Printable keyboard reference (/justscore-cheatsheet.html)
justscore-qr-code.png       ← QR code used in cheatsheet footer
buzzer.wav                  ← Buzzer sound (extracted from index.html in v4.15)
horse.wav                   ← Horse neigh sound (HORSE game)
doh.wav                     ← Bart Simpson doh sound (21 game)
applause.wav                ← Applause sound (winner)
icon-16.png                 ← Favicon (browser tab, small)
icon-32.png                 ← Favicon (browser tab, standard)
icon-48.png                 ← Favicon (Windows taskbar)
icon-72.png                 ← PWA icon (Android legacy)
icon-96.png                 ← PWA icon (Android)
icon-120.png                ← PWA icon (iOS)
icon-152.png                ← PWA icon (iOS iPad)
icon-180.png                ← PWA icon (iOS high-res, apple-touch-icon)
icon-192.png                ← PWA icon (Android standard)
icon-512.png                ← PWA icon (Android splash / Play Store)
```

---

## File Roles and Dependencies

### `index.html` — The App
The entire scoreboard. All game logic, LED rendering, CSS, and HTML in one file.

**References these external files:**
| Reference | Type | Location in file |
|---|---|---|
| `manifest.json` | `<link rel="manifest">` | `<head>` |
| `favicon.ico` | `<link rel="icon">` | `<head>` |
| `icon-180.png` | `<link rel="apple-touch-icon">` | `<head>` |
| `sw.js` | `navigator.serviceWorker.register()` | Bottom of `<script>` |
| `icon-192.png` | `<img src>` in splash screen | HTML body |
| Google Fonts (Oswald) | `<link href>` | `<head>` |

**Contains these version-sensitive strings:**
| String | Location | Must match |
|---|---|---|
| `Release Notes — vX.XX` | Hamburger menu link | Current version |
| URL: `.../releases.html` | Hamburger menu link | Deployed filename |
| URL: `.../help` | Hamburger menu link | Deployed filename |
| URL: `.../justscore-cheatsheet.html` | Hamburger menu link | Deployed filename |

---

### `sw.js` — Service Worker
Controls offline caching. When updated, forces PWA users to receive fresh files.

**Contains these version-sensitive strings:**
| String | Location | Must match |
|---|---|---|
| `const CACHE = 'justscore-vX.XX'` | Line 1 | Current version (use most significant version, e.g. v4.14a not v4.14b) |

**Lists these cached assets (must exist in deployment):**
```
/ /index.html /manifest.json /sw.js /favicon.ico
/icon-72.png /icon-96.png /icon-120.png /icon-152.png
/icon-180.png /icon-192.png /icon-512.png
```
> Note: `icon-16.png`, `icon-32.png`, `icon-48.png` are NOT in the cache list — add if needed.

---

### `manifest.json` — PWA Config
Controls how the app installs on home screens.

**References these icon files:**
`icon-72`, `icon-96`, `icon-120`, `icon-152`, `icon-180`, `icon-192`, `icon-512`

**Contains no version strings.** Only changes if:
- App name or description changes
- Domain/start_url changes
- Icon files change
- Orientation or display mode changes

---

### `releases.html` — Release Notes Page
Human-readable version history. Linked from the hamburger menu in `index.html`.

**Contains these version-sensitive elements:**
| Element | Notes |
|---|---|
| `version-tag current` CSS class | Must be on the LATEST version block only |
| Version blocks (one per release) | Add new block at the TOP for each new version |
| Link back to scoreboard | `https://justscore.justintymesports.net` |
| Links to `help` and `cheatsheet` | Referenced in v4.13 change notes |

**No version string in the filename** — always `releases.html`.

---

### `help.html` — Help Page
Full documentation. Linked from hamburger menu as `Help ↗`.

**Contains:**
- Link back to scoreboard: `https://justscore.justintymesports.net`
- Link to store: `https://www.justintymesports.net`
- Phone number: `888-564-1082`
- No version string — does not need updating on every release
- **Update when:** game presets change, new features added, keyboard shortcuts change, install instructions change

---

### `justscore-cheatsheet.html` — Keyboard Cheat Sheet
Printable one-page reference. Linked from hamburger menu.

**Contains these version-sensitive strings:**
| String | Location | Notes |
|---|---|---|
| `Keyboard Reference • vX.XX` | Header subtitle | Currently showing v4.12 — stale |
| `justscore-qr-code.png` | Footer `<img src>` | QR image not in deployment package — shows fallback text if missing |

**Update when:** keyboard shortcuts change, game presets change, domain changes.

---

### `favicon.ico` and Icon PNGs
Static — never change unless the icon design changes.
All icons are the green LED "2" design in various sizes.
`icon-192.png` is also used in the splash screen inside `index.html`.

---

### `_redirects` — Netlify Redirects
Static — only changes if domain changes.
```
http://justscore.justintymesports.net/*  →  https://justscore.justintymesports.net/:splat
http://justscore.netlify.app/*           →  https://justscore.justintymesports.net/:splat
```

---

### `CHANGELOG.md`
Full project history, strategic context, roadmap, and decisions. Always included in deployment package so it's available on Netlify alongside the app. Drop into any new Claude session to restore context.

---

## Version Update Checklist

Use this checklist every time a new version is built. Check off each item.

### Every Version
- [ ] `index.html` — Update `const CURRENT_VERSION = 'vX.XX'` in JS
- [ ] `index.html` — Verify version menu item label if needed (auto-updates from CURRENT_VERSION)
- [ ] `sw.js` — Update `const CACHE = 'justscore-vX.XX'`
- [ ] `releases.html` — Add new version block at the TOP, move `current` CSS class to new block
- [ ] `CHANGELOG.md` — Add version entry, update `Current version:` line, update `Next:` line
- [ ] `BC product page` — Update version number in About JustScore section (BigCommerce HTML editor)

### When Game Presets Change
- [ ] `help.html` — Update preset specs in Game Presets section
- [ ] `justscore-cheatsheet.html` — Update preset grid

### When Keyboard Shortcuts Change
- [ ] `help.html` — Update keyboard shortcuts section
- [ ] `justscore-cheatsheet.html` — Update key tables

### When Domain Changes
- [ ] `index.html` — All 4 hamburger menu URLs
- [ ] `manifest.json` — `start_url`
- [ ] `sw.js` — No domain references (paths only — no change needed)
- [ ] `_redirects` — Update redirect rules
- [ ] `releases.html` — `btn-launch` href, any inline links
- [ ] `help.html` — All scoreboard URL references
- [ ] `justscore-cheatsheet.html` — URL in header and footer

### When Icons Change
- [ ] Replace all 9 icon files (`favicon.ico` + 8 PNGs)
- [ ] `manifest.json` — Verify icon filenames and sizes still match
- [ ] `sw.js` — Verify cached icon filenames still match ASSETS list
- [ ] `index.html` — `icon-192.png` used in splash screen

### When Help Page Content Changes
- [ ] `help.html` — Content updates only, no version string required

---

## Known Version String Locations — Quick Reference

| File | String | Current Value |
|---|---|---|
| `index.html` | `const CURRENT_VERSION` | `'v4.15'` |
| `sw.js` | Cache name | `justscore-v4.15` |
| `releases.html` | `version-tag current` block | `v4.15` |
| `help.html` | Version badge | `Version 4.15` |
| `justscore-cheatsheet.html` | Header subtitle | `v4.15` |
| `CHANGELOG.md` | `Current version:` | `v4.15` |
| `BC product page` | About JustScore section | Update manually in BigCommerce |

> **Note on sw.js cache name:** Bump whenever `index.html` changes meaningfully. Patch versions that only update supporting files can reuse previous cache name if `index.html` is unchanged.

---

## Build Process — Step by Step

### 1. Start a New Session
Upload to Claude:
- `CHANGELOG.md` — restores all project context
- `JUSTSCORE_BUILD_GUIDE.md` — this file
- `index.html` — current deployed version
- Any other files that will be edited this session

### 2. Define the Version
Decide the version number before writing any code:
- **Major version** (v5, v6) — significant new feature or architecture change
- **Minor version** (v4.15, v4.16) — planned feature from roadmap
- **Patch version** (v4.14a, v4.14b) — bug fix or correction to current minor version

### 3. Make the Changes
Edit files as needed. Use the Version Update Checklist above to identify all affected files.

### 4. Verify Before Zipping
Run these checks before building the zip:

```
1. grep "Release Notes" index.html
   → Should show current version

2. grep "const CACHE" sw.js
   → Should show current or previous version (see note above)

3. grep "version-tag current" releases.html
   → Should show current version block

4. grep "Current version" CHANGELOG.md
   → Should show current version
```

### 5. Build the Zip
Name format: `vXYZ.zip` — no dots except before the extension.
Examples: `v415.zip`, `v414b.zip`, `v414a.zip`

The zip should contain all 19 files flat (no subfolder inside the zip).
Use: `zip -j vXXX.zip foldername/*`

### 6. Deploy via GitHub
1. Upload changed files to GitHub repo (`jptymes/justscore`) via browser
2. Commit message format: `vX.XX — brief description` (under 50 chars)
3. Select **Commit directly to main**
4. Netlify auto-deploys in ~30 seconds — zero credits consumed
5. Verify live URL: https://justscore.justintymesports.net

### 7. Verify Deployment
- [ ] Open scoreboard — confirm it loads
- [ ] Open hamburger menu — confirm version shows correctly (normal or new-version state)
- [ ] Click version link — confirm releases.html opens with v4.15 at top
- [ ] On Android — confirm PWA prompts service worker update (or reinstall)
- [ ] Check browser console for 404 errors
- [ ] Confirm audio plays (start clock, let it run to zero)

---

## File Dependency Map — Visual

```
index.html (PRIMARY)
├── manifest.json         (PWA install)
├── sw.js                 (offline cache — lists index, manifest, favicon, icons)
├── favicon.ico           (browser tab)
├── icon-180.png          (apple-touch-icon in <head>)
├── icon-192.png          (splash screen <img>)
├── Google Fonts CDN      (Oswald font — external, online only)
└── Hamburger menu links:
    ├── releases.html     (Release Notes page)
    ├── help.html         (Help page — contains game/keyboard docs)
    ├── justscore-cheatsheet.html  (Printable keyboard reference)
    └── justintymesports.net       (External store link)

manifest.json
└── icon-72/96/120/152/180/192/512.png  (all 7 PWA icons)

sw.js
└── Caches: index.html, manifest.json, sw.js, favicon.ico,
            icon-72/96/120/152/180/192/512.png

releases.html
├── favicon.ico
├── Google Fonts CDN
└── Links: justscore.justintymesports.net (back to app)

help.html
├── favicon.ico
├── Google Fonts CDN
└── Links: justscore.justintymesports.net, justintymesports.net

justscore-cheatsheet.html
├── Google Fonts CDN
└── justscore-qr-code.png  (NOT in deployment package — shows fallback if missing)
```

---

## Outstanding Issues / Tech Debt

| Item | File | Priority |
|---|---|---|
| Game clock adjustment feature | `index.html` | v4.16 — pending team feedback |
| Remote control / display sync | `index.html` + new backend | v4.16 |
| iOS first test not yet completed | — | Before MailChimp launch |
| MailChimp campaign not yet launched | — | Team availability |
| BC product page version — update to v4.15 | BigCommerce | Do manually now |
| `icon-16/32/48.png` not in `sw.js` ASSETS | `sw.js` | Low — add at next sw.js update |

---

## Platform Test Checklist

Run after any deploy that changes `index.html`:

- [ ] **Desktop Chrome (laptop)** — layout, LEDs, menu, all buttons
- [ ] **Android Chrome (phone, landscape)** — menu scrolls, LEDs render, audio
- [ ] **Android PWA (installed)** — service worker updates, splash screen
- [ ] **Chromebook** — sizing, layout proportions
- [ ] **iOS Safari** — Enable Sound menu item appears, audio unlocks, horn fires
- [ ] **iOS PWA (installed via Share → Add to Home Screen)** — splash, fullscreen

---

*This document should be updated whenever the file structure, dependencies, or deployment process changes.*  
*Keep in sync with CHANGELOG.md.*
