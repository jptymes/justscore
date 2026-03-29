# JustScore — Project Changelog & Strategic Notes

**Product:** JustScore Basketball Scoreboard  
**Company:** JustInTymeSports, LLC  
**Website:** [justintymesports.net](https://www.justintymesports.net)  
**Scoreboard URL:** [justscore.netlify.app](https://justscore.netlify.app)  
**Started:** March 21, 2026  

---

## Strategic Context

### Why JustScore?
JustInTymeSports has manufactured high-quality indoor mini basketball hoops since 1996. JustScore was originally built in 2005 as a companion product to the Mini-Pro hoop line — giving customers a professional scoreboard experience at home or in the gym. Some middle and high schools used the original version with a projector for real games.

JustScore is being revived in 2026 as a **customer stickiness play**, not a monetization effort. The goal is to:
- Keep customers engaged with the JustInTymeSports brand
- Drive traffic to the BC store from the scoreboard
- Provide genuine value to kids and parents who own our hoops
- Create brand exposure when projected in gyms (free advertising)

### Tagline
**Dream Big. Play Hard.**  
Origin story: [justintymesports.net/blog/because-kids-dream-big-and-play-hard](https://www.justintymesports.net/blog/because-kids-dream-big-and-play-hard/)  
Kids aren't just playing a kids game — in their mind they are shooting a buzzer-beater to win the game. JustScore literally lets them simulate that moment.

### Distribution Plan
1. **Existing customers** — MailChimp email campaign to customer list
2. **New customers** — QR code printed on hoop install instructions
3. **BC website** — dedicated JustScore page linking to the app
4. **Word of mouth** — kids sharing the link, gym projector visibility

### Monetization (Future Consideration)
- Possibly create a free Product SKU in BigCommerce so customers "own" it
- Captures email legitimately, shows in order history, enables upgrade path
- Could trigger automated MailChimp welcome email with scoreboard link
- Original model: free with branding, paid to remove branding — may revisit

### Multi-Sport Vision (Long Term)
The scoreboard architecture is designed to support other sports eventually:
- Soccer (count-up clock, no shot clock)
- Hockey (3 periods, penalty box)
- Football (downs, quarters)
- "Dream Big. Play Hard." works for any sport a kid plays

---

## Marketing & Community Ideas

### Hardware & Display Options

JustScore is a browser-based PWA — it runs on virtually any screen with a modern browser. Several hardware paths are worth exploring for wall-mounted or gym display scenarios.

**Immediate / Zero Cost:**
- **Cast from phone** — open JustScore in Chrome on Android, tap the cast icon, display on any Chromecast-enabled TV or monitor. Phone becomes the controller, TV becomes the display. This works *right now* with no additional hardware or development.
- **Laptop via HDMI** — connect to any monitor or projector, open Chrome fullscreen (F11). Already confirmed working for gym/projector use.

**Low Cost Hardware (~$25–$50):**
- **Amazon Fire Stick / Fire TV** (~$25–$40) — plug into any HDMI monitor or TV, runs Silk browser, can run JustScore PWA
- **Chromecast with Google TV** (~$30) — cast tab from Chrome on any device
- **Android TV stick** (~$30–$50) — runs Chrome, PWA installable directly

**Dedicated Kiosk (~$170–$240):**
- **Raspberry Pi 5** (4GB, ~$60) + 24" monitor ($80–$150) + case/power/SD (~$30)
- Runs Chromium browser in kiosk mode — boots directly to JustScore fullscreen, no keyboard or mouse needed
- Most robust and professional option for permanent gym installation
- Pairs perfectly with the Firebase remote control feature (phone controls wall display)

**All-in-One (~$150–$300):**
- **Android smart signage displays** — 24" commercial displays with Android built in (TCL, Vizio, and commercial brands)
- JustScore installs as PWA directly, no extra hardware needed
- Clean single-device solution for permanent installations

**Future Vision:**
When the Firebase remote control feature is built, the full setup becomes:
- Wall-mounted display (Raspberry Pi kiosk or smart display) shows the scoreboard
- Scorekeeper controls everything from their phone
- Crowd sees the big screen, no one needs to touch the display

**Note:** Casting from phone is available *today* — worth promoting in the MailChimp campaign and on the BC site as a feature. "Cast to your TV for the full gym experience."

**Concept:**
- Customers submit short video clips of themselves making a buzzer beater
- Video must include **both** the hoop AND the JustScore scoreboard visible
- Best submissions win loyalty points or products
- Winners featured in the Customer Gallery

**Why it works:**
- Requires both products — JustScore becomes mandatory, not optional
- Directly embodies the brand story — "in their mind they are shooting a buzzer-beater"
- Low cost (loyalty points/products) but high perceived value
- User-generated content = free marketing and social proof
- Videos shared on social extend reach organically

**Content flywheel:**
Kid sets up JustScore → runs shot clock down → makes buzzer beater → records it → submits → JustInTymeSports shares best ones → other kids see it → they want a hoop and scoreboard too

**Things to decide:**
- [ ] Submission mechanism — BC form, email, or social media hashtag (hashtag = lowest friction)
- [ ] Judging criteria — most creative shot, closest to buzzer, best celebration
- [ ] Age categories — e.g. 8-12, 13-17, adult
- [ ] Contest frequency — monthly, seasonal, or launch event
- [ ] Prize structure — loyalty points vs. product giveaway vs. both

**Dependencies:**
- Buzzer Beater game mode must be built before contest launches
- JustScore must be promoted via MailChimp first to build user base
- Customer Gallery page on BC site needs to support video submissions

**Note:** This is a strong reason to prioritize Buzzer Beater mode in the feature roadmap — the contest cannot launch without it.

---

## Technology Decisions

### Hosting
- **Platform:** Netlify (free tier)
- **URL:** justscore.netlify.app
- **Deployment:** Drag and drop folder to Netlify dashboard
- **Future:** Custom domain `scoreboard.justintymesports.net` via DNS CNAME

### GitHub
- GitHub account creation was blocked by inaccessible CAPTCHA puzzles
- Netlify chosen as simpler alternative — drag and drop, no puzzles
- GitHub still worth pursuing for version control — try again from different network
- When ready: create a GitHub Organization (not personal account) — 4 partners

### PWA (Progressive Web App)
- Single HTML file is not sufficient for true PWA install
- Requires 3 files minimum: `index.html`, `manifest.json`, `sw.js`
- Plus icon files: `icon-192.png`, `icon-512.png`
- Confirmed working on Android (Pixel 7) as of v3
- Install: Chrome → three-dot menu → "Add to Home Screen"
- Runs fullscreen with no browser chrome once installed

### Audio
- Original WAV files preserved from 2005 version: `buzzer.wav`, `horse.wav`, `doh.wav`, `applause.wav`
- Embedded as base64 directly in `index.html` — no separate files needed
- Total audio size is small enough to inline cleanly

### Logo
- Current logo is JPG with light background — not ideal on dark scoreboard
- **TODO:** Get transparent PNG version of logo for cleaner watermark and icon
- Current workaround: CSS grayscale + brightness filter on JPG
- PWA icon: red background, white "JS" text (placeholder until real logo PNG available)

---

## Version History

---

## v1 — March 21, 2026
*Quick prototype — single HTML file*

### What Was Built
- Game clock (start/stop/reset) with buzzer sound (Web Audio API generated tone)
- Period tracker — 4 periods, dot indicators, auto-increment
- Score display — +1, +2, +3, −1 buttons for Home and Guest
- Fouls display with +/− controls
- Bonus indicator (hardcoded at 7 fouls)
- Editable team names (contenteditable)
- Period length selector (5, 8, 10, 12 min)
- Full Reset button
- Horn flash animation on clock expiry
- Amber/red/green glowing monospace font aesthetic
- Scanline overlay effect

### What Was Missing (vs. Original JustScore 2005)
- No shot clock
- No game presets (College/Pro/Mini-Pro)
- No keyboard shortcuts
- Foul bonus hardcoded at 7 (not preset-dependent)
- No possession indicators
- No mini-hoop games (HORSE, Twenty-One, Beat-The-Clock)
- No 3rd player support
- No save/load game
- No sound effects beyond generated tone
- Clock only whole seconds (original was 1/10 second under 1 min)
- No custom light colors
- Not responsive on mobile or Chromebook

### Deployment
- Single `scoreboard.html` file, run locally in browser
- Shared directly as a file

---

## v2 — March 22, 2026
*First deployed version — Netlify, PWA attempt*

### What Changed
- **Shot clock** — full display with ▶ ■ ↺ and ↺▶ (reset+start). Turns red at ≤5 seconds
- **Game presets** — College, Pro, Mini-Pro (default), Custom
  - College: 20 min, 2 periods, 35 sec shot clock, 7 fouls bonus
  - Pro: 12 min, 4 periods, 24 sec shot clock, 5 fouls bonus
  - Mini-Pro: 6 min, 4 periods, 12 sec shot clock, 3 fouls bonus (default)
  - Custom: 8 min, 4 periods, 24 sec shot clock, 7 fouls bonus
- **Possession indicators** — amber arrows under each score
- **Keyboard shortcuts** — F5-F9 for clocks, G/H/B/N toggles, S/D/F/A home scoring, J/K/L/; guest scoring
- **Responsive layout** — adapts to portrait/landscape, phone/tablet/Chromebook
- **JustInTymeSports logo** — lower right watermark (JPG with CSS filter)
- **PWA manifest + service worker** — inline blob approach (did not work correctly)
- **Period dots** — correctly hide unused periods (College = 2)
- **Bonus threshold** — now varies by game preset
- **Real audio files** — buzzer, horse, doh, applause embedded as base64
- **Deployed to Netlify** — live URL, drag and drop deployment confirmed

### Issues Found
- PWA installed as browser shortcut, not true app — double address bar, Chrome badge on icon
- Blob-based service worker not recognized by Android Chrome
- LED aesthetic not yet implemented — still using glowing font
- Layout still had top header row consuming vertical space on Pixel 7
- Score digits too close together
- Some elements too dim/transparent (possession arrows, bonus lights)
- Logo watermark interfering with scoreboard area

### Decisions Made
- Netlify chosen over GitHub Pages (GitHub CAPTCHA inaccessible)
- Three-file PWA structure required for proper install
- LED dot-matrix display agreed as target aesthetic
- Guest left / Home right layout matches original

---

## v3 — March 22, 2026
*LED display, proper PWA, hamburger menu, layout overhaul*

### What Changed
- **LED dot-matrix display** — authentic 5×7 dot grid for all major displays
  - Scores: green, 7 rows × 5 cols, large dots
  - Game clock: red, 7 rows × 5 cols, medium dots, red blinking colon
  - Shot clock: red, 7 rows × 5 cols, turns amber at ≤5 seconds
  - Fouls: yellow, 5 rows × 3 cols, smaller dots
  - Period dots: yellow
- **Pure black background** — `#000000` throughout, no gradients
- **White labels** — all element labels (Game Clock, Shot Clock, Fouls, Period, Bonus) now white
- **White divider line** — solid 2px white line between top and bottom panels
- **Hamburger menu** — ☰ top-left, animates to X, slides out flyout panel
  - Game select with checkmark on active game
  - Shop Our Hoops ↗ link to justintymesports.net
  - Help ↗ link to justintymesports.net/support
- **Top header row eliminated** — full vertical space for scoreboard
- **Footer strip** — JustInTymeSports + Dream Big. Play Hard. bottom-left, logo bottom-right
- **Logo** — white/grayscale filter, bottom-right, non-interfering
- **Proper PWA** — real `manifest.json` + `sw.js` files, confirmed installs on Android
- **Red JS icon** — red rounded rectangle, white JS text (placeholder for real logo PNG)
- **Guest left / Home right** — matches original 2005 layout

### Confirmed Working
- PWA installs correctly on Android (Pixel 7) — no address bar, fullscreen
- Address bar issue was caused by improper PWA install in v2 — resolved
- Round orange icon replaced with round red JS icon

### Known Issues / Bookmarked for v4.x
- Fine-tune dot proportions based on Justin/team feedback
- Footer branding size and visibility
- Logo watermark clarity
- Possession arrow visibility

---

## v4.1 — March 23, 2026
*Dot proportions, spacing calibration, label sizing*

### What Changed
- **Rectangular dots** — dots now `height = 1.3 × width` with 40% border-radius, giving classic scoreboard oval/rectangular feel matching the original 2005 app
- **Balanced LED spacing** — middle ground between v3 (too tight) and v4 (too loose):
  - Horizontal gap = 50% of dot width
  - Vertical gap = 55% of dot height
  - Digit gap = 1.2× dot width — clear separation without feeling disconnected
- **Larger labels** — Game Clock, Shot Clock, Fouls, Period, Bonus all significantly larger and bold, matching prominent white label style of original
- **Version number** — footer shows `v4.1` for easy PWA update confirmation
- **Separate CSS vars for dot-w and dot-h** — enables independent horizontal/vertical tuning in future

### Process Notes
- Used side-by-side screenshot comparison (original 2005 vs v4) to identify overcorrection
- v3 was too tight, v4 was too loose — v4.1 targets the middle ground
- Justin feedback pending — will inform v4.2 if further tuning needed
- Adopted major.minor versioning (v4.1, v4.2, etc.) for polish iterations within a major version

### Pending Feedback
- Justin review of v4.1 in progress
- Team feedback on overall direction
- Will inform whether v4.2 is needed or can move to v5 features

---

## v4.2 — March 24, 2026
*Mobile responsiveness, green LED icons, favicon*

### What Changed
- **Full per-platform responsive system** — replaced single breakpoint approach with CSS custom property system. Every size value (dot width, ratio, gaps, padding, label, button) defined as a CSS variable and overridden per device class:
  - Phone portrait (≤480px): smaller dots, 1.12 ratio, tighter spacing
  - Phone landscape (max-height 480px): most compact layout
  - Tablet (600–1024px): medium sizing
  - Desktop/Chromebook (≥1024px): full sizing
  - Auto re-renders on screen rotate/resize
- **Green LED "2" icon set** — full suite of green LED digit icons replacing red JS placeholder:
  - `favicon.ico` — multi-size (16/32/48px) — fixes 404 in Netlify Observability
  - PNG icons: 72, 96, 120, 152, 180, 192, 512px
  - Rectangular dot proportions match app LED style
  - Glow effect on lit dots
- **manifest.json** — updated to reference all 7 PNG icon sizes
- **HTML head** — added `<link rel="icon">` and `<link rel="apple-touch-icon">` tags
- **Changelog included in deployment package** — CHANGELOG.md now ships with each version

### Issues That Prompted This Build
- Phone (Pixel 7) showed overlapping digits, oblong LEDs, layout collisions
- Chromebook looked good — phone needed separate, more conservative sizing
- Netlify Observability showed 404 errors — caused by missing favicon.ico
- PWA icon was red JS placeholder — replaced with on-brand green LED digit

### Deployment Package — 12 files
`index.html`, `manifest.json`, `sw.js`, `favicon.ico`, `CHANGELOG.md`,
`icon-72.png`, `icon-96.png`, `icon-120.png`, `icon-152.png`,
`icon-180.png`, `icon-192.png`, `icon-512.png`

---

## v4.3 — March 24, 2026
*Chromebook layout regression fix*

### What Changed
- **Desktop dot sizes restored** — v4.2 Chromebook was too small; dot sizes now use `clamp()` with vw-based scaling so they grow appropriately on larger screens
- **Desktop ratio increased** to 1.28 — more rectangular on large screens
- **Team name and possession arrow** scale with viewport on desktop
- **Top panel alignment** — team columns and center column now vertically centered, eliminating empty gap in middle of top panel
- **Center column** fills full height for proper vertical distribution

### Issue That Prompted This Build
- v4.2 Chromebook screenshot showed scores much smaller than v4.1
- Large empty gap in top panel between score and bottom of top section
- Desktop breakpoint values were too conservative — needed vw-based clamp() rather than fixed px values

---

## v4.4 — March 25, 2026
*Chromebook sizing fix, version moved to hamburger menu*

### What Changed
- **Chromebook dot sizes fixed** — replaced clamp() with explicit pixel values tuned for 1707×960 Chromebook display. Three clean breakpoints: tablet (600–1023px), Chromebook/desktop (1024–1599px), large desktop (1600px+)
- **Version moved to hamburger menu** — "JustScore v4.4" now appears at the bottom of the flyout menu, subtle and out of the way. Removed from footer strip.
- **Footer strip cleaner** — just JustInTymeSports + Dream Big. Play Hard. No version clutter.
- **Color review noted** — current green (`#00e676`) is lighter than original arcade green. Full color pass deferred to after platform testing is stable. Options: `#00ff41` (matrix green), `#39ff14` (neon green).

### Issues That Prompted This Build
- Chromebook (1707×960) still showing undersized dots in v4.3 — clamp() values were hitting lower bounds
- Version number in footer was too subtle and not the right location
- Switching to explicit px values per breakpoint gives precise control

---

## v4.5 — March 25, 2026
*JavaScript dynamic sizing engine, split layout, round LEDs, white text, full-bleed icons*

### What Changed
- **JavaScript dynamic sizing engine** — proper long-term responsive solution. JS measures actual available pixel space in each LED container after layout, calculates mathematically correct dot size, renders at exactly that size. Works on any screen automatically — phone, tablet, Chromebook, projector, TV.
- **Split layout** — white divider fixed at vertical midpoint. Top half: scores + game clock + period, vertically centered. Bottom half: fouls + shot clock + bonus, vertically centered. Content fills its half naturally on any screen.
- **Round LEDs** — `border-radius: 50%` everywhere. All dots are perfect circles.
- **All text bright white** — menu items, section labels, buttons, brand tag all `#fff`.
- **Consistent label sizes** — Game Clock, Shot Clock, Fouls, Period, Bonus all same `clamp()` size.
- **Foul digit spacing increased** — `digitGapRatio: 1.4` gives more breathing room between digit pairs.
- **Full-bleed icons** — black background fills entire canvas. Android maskable icon no longer shows light edges. Icon dots are perfect circles.
- **Menu section labels white** — GAME, LINKS section headers now white and bold.

### v4.x Candidates (Visual Polish)
- [x] ~~BUG: Game clock colon not lighting up~~ ✅ fixed in v4
- [x] ~~LED "air" fix — off dots invisible~~ ✅ fixed in v4
- [x] ~~Digit spacing too tight~~ ✅ fixed in v4.1
- [x] ~~Larger labels~~ ✅ fixed in v4.1
- [x] ~~Rectangular dot proportions~~ ✅ fixed in v4.1
- [x] ~~Mobile responsiveness — phone layout collisions~~ ✅ fixed in v4.2
- [x] ~~favicon.ico missing — 404 errors~~ ✅ fixed in v4.2
- [x] ~~Green LED icon set~~ ✅ done in v4.2
- [x] ~~Round LEDs~~ ✅ fixed in v4.5
- [x] ~~All text white~~ ✅ fixed in v4.5
- [x] ~~Consistent label sizes~~ ✅ fixed in v4.5
- [x] ~~Foul digit spacing~~ ✅ fixed in v4.5
- [x] ~~Android icon full-bleed~~ ✅ fixed in v4.5
- [x] ~~Dynamic JS sizing engine~~ ✅ implemented in v4.5
- [ ] Color review pass — green, red, yellow, amber (deferred until layout stable)
- [ ] Logo watermark — transparent PNG when available
- [ ] Possession arrow visibility

---

## v4.6 — March 25, 2026
*LED rendering fix, version text white*

### What Changed
- **LED rendering fixed** — v4.5 LEDs were blank on both Android and Chromebook because JS was measuring containers before they had dimensions. Fixed with a robust retry loop (polls every 50ms, up to 40 attempts / ~2 seconds) that waits until containers have real pixel dimensions before rendering.
- **LED containers** given `min-height`, `min-width`, `flex:1`, and `width:100%` so they participate properly in flex layout and give JS something to measure.
- **Team columns** given `width:100%` so LED containers inherit proper width.
- **Version text** in hamburger menu changed to bright white — was unreadable dark gray (`#333`).

### Issues That Prompted This Build
- v4.5 showed correct layout structure but all LED displays blank on both devices
- JS sizing engine was running before flex layout completed — containers reported 0×0
- Version "JustScore v4.5" was invisible in the menu

---

## v4.7 — March 25, 2026
*Layout proportions, landscape fixes, foul size cap, possession arrows repositioned*

### What Changed
- **60/40 split** — top half gets flex:6, bottom half flex:4. Gives scores and game clock more breathing room, fixes Chromebook crowding.
- **Foul dot size capped** — `maxDot: 18` prevents fouls from overwhelming the bottom half. Landscape cap is 14px.
- **Landscape-specific sizing** — `getSizes()` returns smaller maxDot values in landscape: scores 22px, clocks/fouls 14px. Shot clock and game clock match foul height in landscape.
- **Possession arrows moved inside score row** — `score-poss-row` flex container holds arrow + LED side by side, saving vertical space. Guest arrow on left, Home arrow on right.
- **GUEST/HOME label size** — matches Game Clock label in landscape via media query override.
- **Landscape media query** — comprehensive overrides for all elements in landscape/max-height:500px.
- **All labels consistent** — `flex-shrink:0` added so labels don't collapse.

### v4.x Candidates (Features)
- [ ] Custom domain: `scoreboard.justintymesports.net` — set CNAME in DNS, point to Netlify
- [ ] Generate QR code (after domain is finalized) — for MailChimp campaign and install instructions
- [ ] Dedicated Help page on BC site — link from hamburger menu
- [ ] Inline keyboard shortcut reference (? button or overlay)

### Future Versions
- [ ] **Buzzer Beater game mode** ⭐ — *required before contest launch* — shot clock countdown, kid tries to make the shot before the horn
- [ ] Document and promote casting feature — "Cast to your TV for the full gym experience" — include in MailChimp campaign and BC site
- [ ] Mini-hoop games: HORSE (1–6 players, custom word), Twenty-One (2–3 players), Beat-The-Clock
- [ ] Remote control mode — scoreboard on wall tablet, controller on phone (Firebase sync)
- [ ] Save/load game state
- [ ] Sound effects beyond buzzer — horse neigh (HORSE game), Bart Simpson doh (21 game), applause (winner)
- [ ] 3rd player support for Twenty-One and Beat-The-Clock
- [ ] Sub-second clock display (1/10 second) when under 1 minute
- [ ] JustScore free SKU in BigCommerce
- [ ] MailChimp email campaign to existing customers
- [ ] QR code on hoop install instruction sheets
- [ ] GitHub Organization account (4 partners: use business email, org name JustInTymeSports)
- [ ] Android native app (evaluate after PWA adoption)
- [ ] Multi-sport scoreboards (Soccer, Hockey, Football)
- [ ] Per-game-type element visibility — hide/show elements based on game mode
  - Mini-Pro: consider hiding possession arrows (casual home game)
  - College/Pro: show all elements (serious scorekeeping)
  - HORSE: hide game clock, shot clock optional, letter display instead of score
  - Twenty-One: hide periods, special score rules (13=reset, over 21=back to 14)
  - Beat-The-Clock: shot clock only, minimal UI
- [ ] User-controlled display options in hamburger menu (overrides game-type defaults)
  - Toggle: Show/Hide Possession Arrows
  - Toggle: Show/Hide Shot Clock
  - Toggle: Show/Hide Fouls
  - Toggle: Show/Hide Bonus
  - Useful for projector/gym use case — clean minimal display with just scores and clock
- [ ] Keyboard layout review — evaluate all shortcuts against Guest/Home mnemonics
  - G = Game clock toggle (also G = Guest — works on two levels)
  - H = sHot clock toggle (weak mnemonic — consider H = Home possession)
  - Left hand (A/S/D/F) = Guest scoring mirrors left side of scoreboard ✓
  - Right hand (J/K/L/;) = Home scoring mirrors right side of scoreboard ✓
  - Get feedback from anyone who will scorekeeper live games

### Design Notes for Future Reference
- Original 2005 color scheme: scores=green, game clock=red, shot clock=red, fouls=yellow, period=yellow
- Original layout: Guest left, Game Clock center-top, Home right, Shot Clock center-bottom, Fouls bottom-sides
- **LED design principle: negative space is as important as the lit dots** — black between dots makes glowing dots pop. Off dots must be pure black (`#000000`), not dark gray.
- **LED spacing principle: gap between dots should roughly equal dot size** — gives the "air" that makes the display feel authentic and open rather than dense
- "Keep Your Mind On The Goal" was old tagline — retired, do not use
- "Dream Big. Play Hard." is current tagline — use consistently
- Logo should always appear bottom-right on scoreboard, white/grayscale on dark background
- When proper PNG logo is available: update watermark, PWA icon, and consider splash screen

### Process Notes
- This project is following an agile approach — build, share, get real feedback, capture it, iterate
- Screenshot comparisons between original 2005 app and current version have been the most valuable feedback tool
- Changelog serves as the single source of truth for decisions, backlog, and context across sessions
- Drop CHANGELOG.md into any new Claude session to restore full project context instantly

---

## Reference Links
- Live app: [justscore.netlify.app](https://justscore.netlify.app)
- Store: [justintymesports.net](https://www.justintymesports.net)
- Brand story: [justintymesports.net/blog/because-kids-dream-big-and-play-hard](https://www.justintymesports.net/blog/because-kids-dream-big-and-play-hard/)
- Customer gallery: [justintymesports.net/customer-gallery](https://www.justintymesports.net/customer-gallery/)
- Netlify dashboard: [app.netlify.com](https://app.netlify.com)

---

## Team
- John Tymes — john@justintymesports.com
- 3 additional partners (to be added to GitHub Organization when created)

---

*Last updated: March 26, 2026*  
*Current version: v4.8 — milestone build*  
*Next: color review, custom domain, QR code, Buzzer Beater mode*

---

## v4.8 — March 26, 2026
*CSS Grid layout, locked ratios, splash screen, force landscape*

### What Changed
- **CSS Grid layout** — entire scoreboard defined as a single 10-row × 3-column grid. Rows: labels(auto), LEDs(1fr), buttons(auto), divider(2px), labels(auto), LEDs(1fr), buttons(auto), bonus(auto), ctrl(auto), footer(auto). 1fr rows get exactly the remaining space after fixed rows claim their height. LED containers now have mathematically correct dimensions.
- **Locked ratio constants** — all measurements derived from single dot size `d`:
  - `hGap = 0.50 × d` — horizontal gap between dots
  - `vGap = 0.50 × d` — vertical gap between dots (round dots)
  - `digitGap = 0.40 × digitWidth` — inter-digit spacing as ratio of digit width
- **Two font specs** — Large (7×5) for scores/clocks, Small (5×3) for fouls. Digit aspect ratio locked mathematically.
- **Force landscape** — manifest `"orientation": "landscape"`. Portrait shows rotate device message.
- **Splash screen** — CSS overlay shows on launch: green LED icon + JUSTSCORE + by JustInTymeSports + Dream Big. Play Hard. Fades out after 2 seconds.
- **Possession arrows** moved to center column row 3, side by side (◀ ▶) above clock controls.

### Architecture
Grid rows defined once. JS measures each LED cell after grid layout — gets exact available space. calcDot() solves for largest d fitting both W and H constraints. All proportions locked via ratio constants. Works on any screen automatically.

---

## v4.9 — March 26, 2026
*ResizeObserver for LED rendering*

### What Changed
- **ResizeObserver** — replaced polling retry loop with ResizeObserver that fires exactly when each LED cell gets real grid dimensions. Cleaner and more reliable than setTimeout polling.
- **renderLed simplified** — removed retry logic, just returns if container not ready (ResizeObserver handles the retry).

---

## v4.10 — March 26, 2026
*Measure grid cell directly — LEDs finally rendering*

### What Changed  
- **renderLedInCell()** — new function that measures the grid CELL (which has dimensions from CSS Grid) rather than the LED container inside it. This was the root cause of blank LEDs across all previous versions.
- **LED containers** given `width:100%`, `height:100%`, `flex:1` so they fill their cells.
- **Grid cells** given `align-items:stretch` so LED containers inherit full height.
- **LEDs rendering on both Android and Chromebook** ✅ — major milestone.

---

## v4.11 — March 26, 2026
*Chromebook sizing, hamburger clearance, 60/40 split*

### What Changed
- **60/40 split** — top LED row `6fr`, bottom LED row `4fr`. Gives scores more vertical space.
- **Hamburger clearance** — `padding-left: clamp(36px, 4vw, 48px)` on grid prevents left column content being clipped by hamburger menu.
- **Center column wider** — `grid-template-columns: 1fr 1.2fr 1fr` gives game clock more horizontal room.
- **maxDot caps** — `SPECS.large maxDot:22`, `SPECS.small maxDot:12` prevents oversizing on large screens.

### Platform Status
- Android v4.11 — looks great ✅
- Chromebook v4.11 — scores still slightly large, shot clock oversized, but much improved

---

## Pending for v4.12
- [ ] Scale maxDot as percentage of screen height for universal sizing
- [ ] Fix right edge clipping on Android (Home − button)
- [ ] Fix ctrl bar bottom clipping on Android
- [ ] Shot clock maxDot lower to match fouls

---

## Infrastructure — March 26, 2026

### Custom Domain (pending)
- Domain: `justscore.justintymesports.net`
- Steps: Network Solutions → add CNAME `justscore` → `justscore.netlify.app`
- Then: Netlify → Domain Management → Add `justscore.justintymesports.net`
- Then: Update manifest.json `start_url`, regenerate QR code

### QR Code
- Generated for `https://justscore.justintymesports.net`
- Includes green LED "2" icon as center logo
- Included in JustScore User Guide
- Note: Use actual QR scanner to verify when domain is live

### Netlify Bandwidth Note
- Free tier: 100GB/month bandwidth
- Reached 50% mid-March due to heavy testing deploys
- Main driver: base64 audio in index.html (~130KB of 180KB total)
- Future: extract audio to separate files to reduce HTML size

---

## v4.12 — March 28, 2026
*HTTPS fix, footer cleanup, missing icons, _redirects*

### What Changed
- **BC logo removed** — the BigCommerce-hosted logo image (`cdn11.bigcommerce.com`) was causing "broken HTTPS" warning because it was a mixed/cross-origin resource. Removed entirely.
- **Footer redesigned** — JUSTINTYMESPORTS and DREAM BIG. PLAY HARD. moved to right side of footer. Cleaner, no external dependencies.
- **Footer text sizing** — JUSTINTYMESPORTS slightly larger (`clamp(9px,1.5vw,13px)`), tagline proportional. Both use Oswald font directly.
- **Google Fonts fixed** — added `crossorigin` attribute to gstatic preconnect. Fonts load cleanly over https with no certificate warnings.
- **`_redirects` file** — forces http → https redirect and redirects old `justscore.netlify.app` to custom domain.
- **Missing icons added** — `icon-16.png`, `icon-32.png`, `icon-48.png` now included in deployment package.
- **All BC external references removed** — app now has zero external image dependencies.

### Security Note
The "broken HTTPS" warning was caused by the BC logo loading from `cdn11.bigcommerce.com` over a cross-origin connection. Google Fonts (googleapis.com / gstatic.com) load correctly over https and are not the cause. The `_redirects` file ensures all traffic uses https automatically.

### Deployment Package — 17 files
`index.html`, `manifest.json`, `sw.js`, `favicon.ico`, `_redirects`, `CHANGELOG.md`,
`icon-16.png`, `icon-32.png`, `icon-48.png`, `icon-72.png`, `icon-96.png`,
`icon-120.png`, `icon-152.png`, `icon-180.png`, `icon-192.png`, `icon-512.png`
