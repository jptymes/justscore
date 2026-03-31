# JustScore — Project Changelog & Strategic Notes

**Product:** JustScore Basketball Scoreboard  
**Company:** JustInTymeSports, LLC  
**Website:** [justintymesports.net](https://www.justintymesports.net)  
**Scoreboard URL:** [justscore.justintymesports.net](https://justscore.justintymesports.net)  
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
- **URL:** justscore.justintymesports.net (custom domain, live as of v4.12)
- **Deployment:** GitHub → Netlify auto-deploy (connected March 31, 2026)
- **Previous deployment method:** Drag and drop zip to Netlify dashboard — retired
- **Netlify deploy credits:** 28 remaining as of March 31 — no longer consumed via GitHub integration
- **SSL:** Netlify-managed, auto-renewing, covers custom domain ✅
- **Analytics:** Available in Netlify dashboard ✅

### GitHub
- **Account:** github.com/jptymes (personal account — jptymes)
- **Repository:** github.com/jptymes/justscore (public, HTML)
- **Branch:** main
- **Connected to Netlify:** Yes — auto-deploys on every push to main ✅
- **Current repo contents:** v4.14b — 20 files + JUSTSCORE_BUILD_GUIDE.md + README.md
- **Git client:** Not yet installed locally — browser uploads used for now
- **Organization:** Not yet created — plan to create JustInTymeSports org and transfer repo when 4 partners are ready
- **Previous blocker:** GitHub account creation was blocked by inaccessible CAPTCHA — resolved by trying from different network
- **Deploy process going forward:**
  1. Make changes locally
  2. Upload changed files to GitHub via browser (Add file → Upload files)
  3. Commit message format: `vX.XX — brief description`
  4. Netlify auto-deploys in ~30 seconds
  5. Zero credits consumed

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
- [ ] **Extract audio files from HTML** ⭐ — currently buzzer.wav, horse.wav, doh.wav, applause.wav are base64-encoded inside index.html adding ~130KB to every page load. Extract to separate files so browsers cache them after first visit. Will reduce HTML from ~180KB to ~50KB and significantly cut Netlify bandwidth usage at scale. Priority before MailChimp campaign launch.
- [ ] **Buzzer Beater game mode** ⭐ — *required before contest launch* — shot clock countdown, kid tries to make the shot before the horn
- [ ] Document and promote casting feature — "Cast to your TV for the full gym experience" — include in MailChimp campaign and BC site
- [ ] Mini-hoop games: HORSE (1–6 players, custom word), Twenty-One (2–3 players), Beat-The-Clock
- [ ] Remote control mode — scoreboard on wall tablet, controller on phone (Firebase sync)
- [ ] Save/load game state
- [ ] **Scoreboard sharing via Teams / Google Meet** — user shares JustScore screen in a video call. Remote grandparents watch grandkids play live with a real scoreboard. Grandparents in Florida, grandkids in Grand Rapids — in real time. Technically trivial (screen share is built into every platform) — the opportunity is documenting and promoting this use case. Major brand story moment.
- [ ] **JustMove** — brand extension concept. Same philosophy as JustScore applied to broader physical activity. "Keep Your Mind On The Goal." Bookmark for future brand strategy discussion.
- [ ] **"What's Your Goal?"** — original JustInTymeSports tagline, retired as primary but not forgotten. Could live again as a campaign, youth program, or product line. The dual meaning (basketball goal / life goal) is still powerful in the right context.

---

## March 30, 2026 — Remote Control Use Case & Display Sync

### The Core Problem Identified

Current JustScore architecture requires one device to be both controller AND display. When scoreboard is mounted high on wall (near hoop), the person controlling the score has to look down at their phone — breaking the game experience.

**The ideal setup:**
```
High on wall near hoop:
[JustInTymeSports hoop]
[JustBoard display — tablet or small TV]
[Scoreboard visible to all players]

In hand:
[Phone as controller]
[Tap to score, start/stop clock]
[No need to look at phone — score is on the wall]
```

This use case is fundamental to the JustBoard display station concept, the break room deployment, and the classroom deployment.

### Solutions — Current and Future

**Works TODAY — Chromecast to Small TV:**
```
Phone running JustScore
Cast to small TV or monitor near hoop
Phone controls everything
TV displays everything — visible to all players
```
- 24" TV with built-in Chromecast: $129-179
- Any TV + Chromecast dongle ($35): most cost effective
- Amazon Fire TV Stick on any HDMI monitor: $35+
- Wall mount near hoop: $15-25
- Best current solution for break room and classroom
- No new development needed

**Future — Remote Control / Display Sync (PRIORITY ELEVATED):**

Option A — Game Code Sync (simpler, recommended):
```
Device 1: Tap [Share Game] → generates code: 4729
Device 2: Enter code 4729
Both connected to same game state via WebSocket
Either device can control
Changes sync in real time
```
Simple 4-digit game code. No account. No Firebase complexity. Lightweight WebSocket sync. Elegant and on-brand (private, simple, no friction).

Option B — Firebase sync (more complex, more robust):
```
Full real-time database sync
Multiple controllers possible
More infrastructure required
```

### Revised Development Priority

```
v4.13: Footer, help page, cheatsheet ✓ DONE
v4.14: Android clipping fixes (right edge, ctrl bar)
v4.15: Remote control / display sync ← ELEVATED
        Game code approach recommended
        Unlocks JustBoard product concept
        Enables break room / classroom deployment
v4.16: Buzzer Beater game mode
v4.17: What's Your Goal? feature
v4.18: JustMove platform
```

### JustBoard Display Station — Product Concept

A tablet/phone mount that matches JustInTymeSports backboard aesthetic:

**Design language:**
- Polycarbonate face
- Steel or 3D printed frame
- Orange accent details
- JustInTymeSports branding
- "WHAT'S YOUR GOAL?" or "JUSTSCORE" router engraved
- Mirrors backboard family visual language

**Manufacturing paths:**
- Option A: Laser cut steel frame + poly face (existing vendor)
- Option B: 3D printed frame + poly face (prototype path)
- Option C: Full Color Core HDPE (neighbor vendor)
- Recommend: 3D print prototype first, laser/Color Core for production

**Product line:**
```
JustBoard Phone Mount
JustBoard Tablet Mount (7-8")
JustBoard Tablet Mount (10")
Available in team colors via Color Core
Custom engraving: "WHAT'S YOUR GOAL?" etc.
```

**Break room complete package:**
```
JustInTymeSports hoop (customer choice)
+ JustBoard display station
+ Small TV or tablet
+ JustScore (free, pre-configured)
+ "WHAT'S YOUR GOAL?" backboard option
Price: $399-599 installed
Corporate bulk pricing available
```

**Classroom complete package:**
```
Mini Pro 2.0 hoop
+ JustBoard display station
+ STEM activity worksheets
+ Teacher guide
+ JustScore (free)
Price: $299-399
Grant eligible: Physical activity + STEM + SEL
```

### Phone to Tablet Casting — Research Summary

Native casting from phone to tablet is NOT built into Android or iOS. Requires third party apps:
- AirDroid Cast — most versatile, free basic tier
- Samsung Flow — Samsung devices only, works well
- Miracast — if both devices support it

**Recommendation:** Don't cast phone to tablet for JustBoard. Run JustScore directly ON the tablet. Use remote control sync feature (v4.15) for phone-as-controller when built. Until then — Chromecast to TV is the best wall display solution.

### llm.txt — Rave Capture Integration

Rave Capture responded with calendar invite and suggested llm.txt and llms-full.txt files — emerging standard for AI/LLM content discovery.

**What these files do:**
- Structured content files readable by AI language models
- Similar to robots.txt but designed for AI systems
- Makes reviews, descriptions, and content directly AI-readable
- Closes the JavaScript invisibility gap for 1,880 reviews

**Implementation:**
- Text files uploaded to root domain
- justintymesports.net/llm.txt ← ideal (BC file upload)
- justscore.justintymesports.net/llm.txt ← fallback (Netlify)
- No developer needed if BC allows static file uploads
- Rave Capture calendar meeting scheduled — confirm details

**Action items:**
- [ ] Attend Rave Capture meeting — confirm llm.txt content and update frequency
- [ ] Upload llm.txt to BC root if supported
- [ ] Add llms-full.txt with complete review content
- [ ] Add Rave Capture help doc link to changelog when available
- [ ] Confirm BC supports HTML file uploads for instruction pages
- [ ] If confirmed — build mobile-optimized HTML instruction pages per hoop model

---

## March 30, 2026 — Brand Philosophy Session

### The Core Discovery

Today's conversation surfaced the deepest articulation of the JustInTymeSports brand philosophy to date. These insights emerged organically from a story about Justin's oldest boy (the boy in glasses) watching MSU's Cohen Carr make a brilliant baseline save — then going downstairs to practice that exact move on his JustInTymeSports hoop — then making it in a real game.

**The two lines that define everything:**

*"The goal is the dream in process."*
*"We teach kids how to dream."*

These are not marketing copy. They are a truth that has played out in the Tymes family across three generations — and in every kid who ever walked past a craft show booth and whose face changed when they saw the hoops.

---

### JustScore — Reframed

JustScore is not a scoreboard app. It is a **youth development platform disguised as a game.**

```
Kids think:       "I'm playing basketball"
What's happening: "I'm setting goals, tracking progress,
                   building skills, measuring improvement,
                   learning to dream bigger"
```

The best learning never feels like learning.

**The platform stack:**
- **JustScore** — the game (scoreboard, clock, real competition)
- **What's Your Goal?** — the dream (set it, name it, own it)
- **JustMove** — the body (track activity, movement, progress)
- **The Gallery** — the achievement (share when YOU choose)
- **The Recording** — the proof (your moment, your story)

---

### The Privacy Principle — Core Differentiator

```
No algorithm deciding what gets seen
No strangers commenting
No likes to chase
No comparison to others
No data sold
No account required

Just:
A kid. A goal. A hoop.
Progress that belongs to them.
Share only what and when you want.
```

This is a genuine differentiator from every platform targeting kids in 2026.

**The parent pitch:**
```
Social media:  Public. Permanent. Algorithmic. Addictive.
JustScore:     Private. Local. Purposeful. Physical.
```

**The screen time reframe:**
- "Not screen time. Development time."
- "The only platform that makes kids put down the phone and pick up a ball."

---

### The Screen Share / Recording Discovery

JustScore + Google Meet/Teams screen share + camera on = free game recording platform.

**What this enables:**
- Grandparents watch live games remotely (scoreboard + camera simultaneously)
- Game recording with scoreboard overlay — no equipment needed
- Buzzer Beater contest entries — verifiable, authentic, impossible to fake
- Dream Big. Play Hard. Gallery Contest entries

**The contest submission path:**
```
Start Meet/Teams call
Share JustScore screen
Turn camera on → captures the game
Hit Record
Play ball
Submit recording to DBPH Gallery Contest
```

No GoPro. No editing software. No third party app. Free. Works today.

---

### What's Your Goal? — The Feature

A goal-setting and tracking feature within JustScore/JustMove:

```
Kid opens app
Enters their goal:
  - Score 50 points in one game
  - Make 10 free throws in a row
  - Do 100 pushups this week
  - Run a mile / walk 10,000 steps
  - Master the Cohen Carr baseline save
Tracks progress
Saves locally per player — private, no account
Celebrates when achieved
```

**Key principle:** Local storage only. No server. No account. No data shared unless the kid chooses. Completely private by default.

**The curriculum:**
- What's Your Goal? = names the dream
- JustScore = makes the practice real
- JustMove = tracks the body
- The Gallery = celebrates the achievement

---

### The Cohen Carr Loop

The complete dream-to-achievement cycle, named after the moment that revealed it:

```
Watch    → Cohen Carr makes a brilliant baseline save on TV
Dream    → "I can do that" — What's Your Goal?
Practice → JustInTymeSports hoop, downstairs, alone
Achieve  → Makes the same save in a real game
Record   → Meet/Teams screen share + camera
Share    → DBPH Gallery Contest, if they choose
```

This loop is what JustInTymeSports has enabled since 1996. The digital platform makes it visible, trackable, and shareable — without changing what it fundamentally is.

---

### The Competitive Landscape

Nobody owns this space:

```
Peloton:          Adult fitness, subscription, expensive
Nike Training:    Adult, generic, no real community
Youth sports apps: Team focused, coach driven, public
Social media:     Dangerous for kids, algorithmically addictive

JustScore:        Kid driven, private, free, physical,
                  goal-oriented, family connected,
                  Made in America by a family that has been
                  teaching kids to dream since 1996
```

---

### The Business Philosophy

**Free forever:** Core scoreboard — always. Non-negotiable. It is the thank you.

**Optional future layers:**
- Premium goal tracking features
- School / YMCA institutional licenses
- Coach team goal dashboards
- Brand partnerships aligned with youth development (not ads)

None of these compromise the privacy principle. All optional. Core always free.

---

### The Brand Statement

*JustInTymeSports builds the tools that turn dreams into goals and goals into achievements. The hoop is where it starts. JustScore is where it gets real. What's Your Goal is where kids learn the most important skill of all — how to dream on purpose.*

*Private. Free. Physical. Fun.*

*Dream Big. Play Hard.*

---

### The T-Shirt

The cartoon image of Justin's boys — "DREAM BIG. PLAY HARD." on the shirt — is now a merchandise line:

```
Kids sizes      — cartoon image, DREAM BIG. PLAY HARD.
Adult sizes     — for parents and coaches
Youth leagues   — bulk orders for teams
Justin's YMCA teams — natural distribution
Contest prize   — included with Dream Big. Play Hard. hoop
```

Need more shirts. 😄

---

### Key Phrases Coined Today — Do Not Lose These

- **"The goal is the dream in process."**
- **"We teach kids how to dream."**
- **"Not screen time. Development time."**
- **"Share only what and when you want."**
- **"The only platform that makes kids put down the phone and pick up a ball."**
- **"Private. Free. Physical. Fun."**
- **"The Cohen Carr Loop"** — watch → dream → practice → achieve → record → share

---

### Action Items from This Session

- [ ] Share "The goal is the dream in process / We teach kids how to dream" with Justin and Jeremy — get family input
- [ ] Consider adding these lines to About Us and Mission
- [ ] Draft "What's Your Goal?" feature spec for JustScore roadmap
- [ ] Blog post: "How to Record Your Kids' Basketball Games for Free"
- [ ] Blog post: "How to Share JustScore with Family on Video Calls"
- [ ] Blog post: "What's Your Goal? How We Teach Kids to Dream"
- [ ] Explore T-shirt production — cartoon image, DBPH tagline
- [ ] Check inventory on Dream Big. Play Hard. Limited Edition hoop — contest prize candidate
- [ ] Define DBPH Gallery Contest structure and submission process
- [ ] JustMove — begin feature definition when JustScore stable
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

*Last updated: March 31, 2026*  
*Current version: v4.14a*  
*Next: v4.15 — Android clipping fixes (Home − button right edge, ctrl bar bottom)*

---

## v4.14a — March 31, 2026
*iOS audio unlock — moved to menu, removed floating banner*

### What Changed
- **Floating audio unlock banner removed** — the "🔊 Tap to Enable Sound" amber banner introduced in v4.14 was overlapping the ctrl bar buttons (STOP, ↺ CLOCK), blocking controls. Removed entirely.
- **iOS-only menu item added** — "🔊 Enable Sound" now appears as the first item in the hamburger menu, above the Game section, but only on iOS devices (detected via user agent + `maxTouchPoints`). Tapping it unlocks audio and closes the menu. The item disappears after unlock.
- **Non-iOS devices unaffected** — Android and desktop never see the menu item. Zero UI change for them.
- **iPad detection included** — newer iPads report as desktop Safari but have `maxTouchPoints > 1`; handled correctly.
- **Version updated** — Release Notes menu link updated to v4.14a.

### Why v4.14a vs v4.15
The floating banner was a usability regression introduced in v4.14. Patching it as v4.14a keeps the v4.15 slot reserved for the planned Android clipping fixes.

### Deployment — 2 files changed
Only `index.html` and `CHANGELOG.md` changed from v4.14. All other 17 files unchanged.

---

## v4.14 — March 30, 2026
*Menu scroll fix, iOS audio unlock*

### What Changed
- **Menu scroll fix** — hamburger flyout menu now scrollable on small screens. Added `overflow-y: auto`, `max-height: 100%`, and `-webkit-overflow-scrolling: touch` to `#flyout`. Previously the menu was clipped on Android phones in landscape — Links section and below were unreachable.
- **iOS audio unlock** — iOS Safari requires audio to be triggered within a user gesture call stack. Clock horn and shot clock buzzer were silently blocked on iOS because they fire from a `setInterval` callback, not directly from a tap. Fix: on first `touchstart` anywhere on screen, all audio elements are primed with a silent play/pause. After this one-time unlock, all programmatic audio (horn, buzzer) fires correctly. A small amber "🔊 Tap to enable sound" indicator appears on launch and auto-dismisses after the first tap.
- **Version updated** — hamburger menu Release Notes link updated to v4.14.

### iOS Compatibility Notes (first iOS test planned)
- Audio unlock resolves the primary known iOS blocker
- PWA install on iOS requires Share → Add to Home Screen in Safari (no auto-prompt like Android)
- `help.html` iOS install instructions should be verified/updated
- `contenteditable` team names will trigger iOS keyboard — may cause layout reflow, worth testing
- All other elements (CSS Grid, ResizeObserver fallback, touch-action, user-select) already iOS-compatible

### What Prompted This Build
- Android testing revealed menu cut off below Links section in landscape
- iOS testing not yet started — audio unlock added proactively before first iOS test

### Deployment Package — 19 files (unchanged from v4.13)
`index.html`, `manifest.json`, `sw.js`, `favicon.ico`, `_redirects`, `CHANGELOG.md`,
`help.html`, `justscore-cheatsheet.html`, `releases.html`,
`icon-16.png`, `icon-32.png`, `icon-48.png`, `icon-72.png`, `icon-96.png`,
`icon-120.png`, `icon-152.png`, `icon-180.png`, `icon-192.png`, `icon-512.png`

### Still Pending
- [ ] Android right edge clipping (Home − button) → v4.15
- [ ] Android ctrl bar bottom clipping → v4.15
- [ ] Extract audio files from HTML (reduces ~180KB → ~50KB)
- [ ] iOS first test — verify audio unlock, PWA install, team name keyboard behavior
- [ ] Update `help.html` with iOS-specific PWA install instructions
- [ ] `releases.html` — add v4.14 entry

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

---

## v4.13 — March 30, 2026
*Footer fix, Help page, Cheat Sheet, Release Notes page, updated menu*

### What Changed
- **Footer layout fixed** — "Dream Big. Play Hard." now on LEFT, JustInTymeSports on RIGHT. Changed `justify-content` from `flex-end` to `space-between` and swapped HTML element order.
- **DBPH color** — removed `opacity:0.5` from `#brand-tag`. Text is now full white — more visible and consistent with brand presentation.
- **Help link updated** — hamburger menu Help button now points to `https://justscore.justintymesports.net/help`
- **help.html deployed** — full help page now live at `justscore.justintymesports.net/help`
- **justscore-cheatsheet.html deployed** — printable keyboard cheat sheet with QR code
- **releases.html** — new release notes page at `justscore.justintymesports.net/releases.html`. Covers v1.0 (2005) through v4.13. Each entry has typed badges: Fix, New, Update, Design.
- **Hamburger menu updated** — version number removed from bottom of menu. Links section now reads:
  - Shop Our Hoops ↗
  - Help ↗
  - Keyboard Cheat Sheet ↗
  - Release Notes — v4.13 ↗
- **flyout-version CSS** — set to `display:none` (element kept for compatibility, hidden)
- **Service worker** updated to `justscore-v4.13`

### Deployment Package — 19 files
`index.html`, `manifest.json`, `sw.js`, `favicon.ico`, `_redirects`, `CHANGELOG.md`,
`help.html`, `justscore-cheatsheet.html`, `releases.html`,
`icon-16.png`, `icon-32.png`, `icon-48.png`, `icon-72.png`, `icon-96.png`,
`icon-120.png`, `icon-152.png`, `icon-180.png`, `icon-192.png`, `icon-512.png`

### Note on file count
19 files total — earlier references to "20 files" were a miscount. 19 is correct.

### BC Product Page
- Add link to releases.html from BC product page description
- Suggested text: "JustScore is actively developed and updated. View release notes and version history →"

### Still Pending (future versions)
- [ ] Android right edge clipping (Home − button)
- [ ] Android ctrl bar bottom clipping
- [ ] maxDot scaling as % of screen height (held — some risk)
- [ ] Extract audio files from HTML (reduces 180KB → ~50KB)
- [ ] BC Support page — add link to help.html
- [ ] Self-hosted logo PNG when available

---



### New Files Created (ready for v4.13 deployment)

**help.html** — Full help page for `justscore.justintymesports.net/help`
- Matches JustScore dark theme exactly — same Oswald font, amber/green/red color palette, LED aesthetic
- Sticky header with Shop Hoops and Open Scoreboard buttons
- Navigation pills for quick section jumping
- Sections: Quick Start (4 steps), Install (Android/iPhone/Chromebook/Cast to TV), Game Presets (all 4 with specs), Controls (all elements explained), Keyboard shortcuts (complete), FAQ (10 questions, expandable), Contact
- Mobile optimized, no external dependencies beyond Google Fonts
- Footer: Dream Big. Play Hard. / JustInTymeSports / Grand Rapids / Since 1996

**justscore-cheatsheet.html** — Printable one-page keyboard reference
- Black header / white body / black footer — prints cleanly on letter paper
- All keyboard shortcuts in two-column layout
- All four game presets in a grid with full specs
- Memory tip for guest/home key layout
- QR code in footer (references `justscore-qr-code.png` — must be in same folder)
- Print button shown on screen, hidden on print
- Fits on one US letter page

### Help Link — Pending v4.13 Update
- Current: hamburger menu Help link → `https://www.justintymesports.net/support`
- Update to: `https://justscore.justintymesports.net/help`
- Also update: BC Product page Help link, BC Support page link

### Deployment Notes
- Add `help.html` and `justscore-cheatsheet.html` to Netlify folder alongside `index.html`
- Both files are ready — held for deployment until Netlify bandwidth resets
- QR code PNG must be in same directory as cheatsheet for footer image to load

---

## March 29, 2026 — Brand, Marketing & Product Strategy Session

### Brand Documents Updated/Created

**About Us Rewrite (Word doc)** — `JustInTymeSports_About_Us.docx`
Full rewrite incorporating all new story elements. Sent to family for review.
- Jeremy's full story — website at 14, partner, specific roles, personal review note embedded
- Garage manufacturing detail — hand-welding frames, Justin tying nets by hand
- Craft show moment — basketball kids whose faces changed
- Before/after photo section — Justin's AI-enhanced photos of his boys
- Extreme Makeover fully documented — Walker Family, December 2 2011, Ray Allen (Boston Celtics), all three Kardashians, Demi Lovato, Cody Simpson, Springfield MA, 111,000+ anti-bullying pledges, no invoice sent
- Make-A-Wish donation referenced
- Vision and Mission — approved March 2026
- By the Numbers — expanded timeline including tagline origin and Extreme Makeover
- Pull quotes throughout, publishing notes in yellow boxes
- Giving Back section — dignity-first approach, told from JustInTymeSports side only

**AEO Addendum** — `JustInTymeSports_AEO_Addendum.docx`
Supplements original AEO audit with:
- Vision and Mission formally documented
- All brand story elements catalogued with AEO value ratings
- Rave Capture discovery — 1,880 reviews, 4.9 stars, 9.9/10 TrustScore, 91% five-star
- Visibility audit — reviews and Customer Gallery are JavaScript-loaded, invisible to AI crawlers
- Rave Capture company page (app.ravecapture.com/store/JustInTymeSports) IS crawlable — link from main site
- Five standout reviews worth featuring as static text
- Photo archive catalogued with best use for each image

### Vision & Mission — APPROVED March 29, 2026

**Vision:**
*A hoop on every wall. A dream in every kid. A scoreboard to make it real.*

**Mission:**
*To build the highest quality indoor basketball hoops in America — and everything that makes the dream come alive around them. Because we've seen it since 1996. The focus. The persistence. The progress. The moment a kid picks up a ball and stops seeing a basement — and starts seeing an arena. That moment is real. We build products for that moment. And JustScore, our free digital scoreboard, is our way of saying thank you for dreaming.*

**Tagline notes:**
- "Dream Big. Play Hard." — primary tagline, 30 years of equity, do not change
- "Live the Dream" — use subtly as subtext where appropriate, NOT as a primary tagline
- Original tagline "What's Your Goal?" — retired, do not use

### Brand Story Elements — Confirmed Today
- **Origin:** Justin at 9, broken hoop, plexiglass in basement, 1996
- **Tagline origin:** "Dream Big. Play Hard." came from watching kids at craft shows — the focus, learning, persistence, and progress. Replaced "What's Your Goal?" which was too nuanced.
- **Craft shows:** Basketball kids' faces changed the moment they saw the hoops — already somewhere else in their minds
- **Jeremy:** Built first website at 14. Now a partner — tech, assembly, shipping, always a supporter. 5 years younger than Justin.
- **Justin's boys:** Ages 7 and 8, grabbed phone to use JustScore, ran downstairs. Same age Justin was in 1996. Third generation.
- **Extreme Makeover:** Walker Family episode, December 2 2011, ABC. Springfield MA. Ray Allen (not Allen Iverson — confirmed). All three Kardashians, Demi Lovato, Cody Simpson. 111,000+ anti-bullying pledges. Hoops donated, no invoice. Grand Rapids Press article December 3 2011 — SCAN IMMEDIATELY, only known physical record.
- **Make-A-Wish:** Donated hoops, no invoice. Details TBC with Justin.
- **JustScore as philosophy:** Free by design. "The dream shouldn't cost anything extra." Our way of saying thank you for dreaming.

### Photo Assets — Identified and Catalogued
- Justin & Jeremy at Grand Rapids Sports Hall of Fame booth (late 1990s) — About Us hero
- Craft show car trunk — family hustle
- Garage weld shop — Made in USA proof
- Grand Rapids Drive halftime — hoop in professional arena, packed crowd
- Gus Macker custom hoop — community partnership
- Detroit Pistons / Extreme Makeover — donation story
- Justin's AI-enhanced photos of his boys:
  - Cartoon version — "Dream Big. Play Hard." on shirt, defender/shooter, brand mascot candidate
  - Realistic edit — same boys, red carpet/grey wall replaced with hardwood court + three-point line
  - Original photo — boys playing in actual JustInTymeSports facility (same red carpet and grey wall)
- **KEY INSIGHT:** Before (original) / After (realistic edit) = most powerful marketing image. Shows what the kid really sees vs. what's actually there. "What they see. What they feel." Homepage hero candidate.
- Grand Rapids Press article December 3 2011 — physical newspaper, only known record of Extreme Makeover story. SCAN AT HIGH RESOLUTION IMMEDIATELY.

### Rave Capture — Critical AEO Finding
- **1,880 total reviews** — 4.9 stars, 9.9/10 TrustScore, 10/10 Recommend, 91% five-star
- Reviews on justintymesports.net product pages: JavaScript-loaded, **invisible to AI crawlers**
- Customer Gallery on justintymesports.net: JavaScript-loaded, **invisible to AI crawlers**
- Rave Capture company page (app.ravecapture.com/store/JustInTymeSports): static HTML, **visible to AI** ✓
- Action: Link to Rave Capture page from homepage and product pages
- Action: Publish "What Our Customers Say" blog post with top reviews as static text
- Action: Contact Rave Capture about AI/crawler visibility — message sent March 29
- Action: Update Rave Capture About Us text to match new rewrite

### JustScore Product Page — BC
- Rough draft created in BigCommerce
- Hero image: multi-device mockup (phone, tablet, two laptops) with real hoop in background — created by John using Gemini
- Price: $0.00 ✓
- Help link will point to `justscore.justintymesports.net/help` when deployed
- "PWA Beta" watermark to be removed from hero image before final launch

### Product Innovation — Discussed
Full details in product development notes. Key decisions:

**Eyelet Redesign:**
- Current: welded curl eyelet, ~1/2" standoff, outsourced to spring/die company
- Problem: lever arm causes fatigue failure from dunk forces
- New design: laser cut U-shaped rectangle, 10ga steel, 1/4" × 1" approx, slot cut for net retention
- Standoff reduced to ~3/16" — dramatically reduces bending moment
- Two welds along full bottom edge — maximum weld surface
- Net knot self-retains in slot — no retainer clip needed for nylon nets
- Chain nets: chain link hooks over top edge before welding
- Prototype path: send DXF to existing laser vendor, tumble, weld to test ring
- Same vendor as frames — no new relationships needed
- Potential to bring eyelet production in-house vs. spring/die company

**3D Printing Opportunities:**
- Airless mini basketball in TPU — Wilson Airless Gen 1 is full-size precedent
- Retainer clips for eyelet system
- JustScore phone/tablet mount
- Court line markers (snap-on floor markers)
- Net production evaluated — small net (12") fits standard printer, large net (16") requires large format
- Net cost analysis: import $0.50 vs domestic $10+ vs 3D print $1.50-3.00
- Recommendation: continue importing standard nylon; chain net as domestic premium; 3D print as future option
- 5,000+ nets/year requirement = ~20/working day; 2-3 printers could theoretically supply all

**Shot Detection for JustScore:**
- Goal: detect made shots automatically, auto-score, stop shot clock
- Recommended: IR beam break + ESP32 + Bluetooth
- IR emitter/receiver across rim: $3-5
- ESP32 microcontroller: $5-8
- 3D printed housing: $1-2
- Total: ~$12-20 per hoop
- Product: "JustScore Sensor Kit" — $29-49 retail
- Enables Buzzer Beater contest with verifiable auto-scored results
- Bluetooth pairs with JustScore on phone

### Marketing — Key Items
- Blog Posts 1, 2, 3 drafted — ready to publish
- Marketing Plan document complete — timing adjusted to early April (team out, tax season)
- AEO Audit complete + Addendum added
- MailChimp + BigCommerce integration — priority when team available
- Post-purchase email sequence — draft when team available
- Before/after photo campaign — pending Justin sharing AI-enhanced photos
- Cartoon image of Justin's boys — brand mascot candidate, "Dream Big. Play Hard." on shirt

### Immediate Actions (Early April)
- [ ] Scan Grand Rapids Press article (Dec 3 2011) at high resolution — URGENT
- [ ] Family review of About Us Word doc — email thread active
- [ ] Jeremy to review his section of About Us
- [ ] Justin to confirm Ray Allen (not Allen Iverson) for Extreme Makeover episode
- [ ] Justin to share AI-enhanced photos for marketing use
- [ ] Update Rave Capture About Us text to match new rewrite
- [ ] Await Rave Capture response on AI/crawler visibility
- [x] ~~Deploy help.html and cheatsheet when Netlify bandwidth resets~~ ✅ Done v4.13
- [x] ~~Update hamburger menu Help link to new help.html URL~~ ✅ Done v4.13
- [ ] Laser cut eyelet prototype — send DXF to vendor
- [ ] Remove "PWA Beta" watermark from BC product page hero image
- [ ] Install Git locally — enables command line push to GitHub vs browser upload
- [ ] Create JustInTymeSports GitHub Organization when 4 partners ready — transfer repo

---

## March 31, 2026 — Infrastructure Session

### GitHub + Netlify Pipeline — COMPLETE ✅

- **GitHub account created:** github.com/jptymes (personal account)
- **Repository created:** github.com/jptymes/justscore (public)
- **v4.14b uploaded to GitHub:** 20 deployment files + JUSTSCORE_BUILD_GUIDE.md + README.md
- **GitHub connected to Netlify:** Auto-deploy on push to main branch ✅
- **Netlify team name:** JustInTymeSports (auto-detected from account)
- **Deploy credits:** No longer consumed — GitHub integration uses zero credits
- **Custom domain and SSL:** Unchanged — still fully active on Netlify ✅
- **Site analytics:** Still available in Netlify dashboard ✅

### Deploy Process — Updated
Old process: Edit files locally → zip → drag and drop to Netlify (consumes 1 credit)
New process: Edit files locally → upload to GitHub → Netlify auto-deploys in ~30 seconds (zero credits)

### Build Guide Created
`JUSTSCORE_BUILD_GUIDE.md` — file map, dependency chart, version update checklist, build and deploy instructions. Added to GitHub repo and project documents. Reference in every future session alongside CHANGELOG.md.

### Deployment Package — Updated to 20 Files
`justscore-qr-code.png` added — was missing from all previous packages. Cheatsheet footer QR code now renders correctly. All future packages = 20 files.

### Pending Infrastructure
- [ ] Install Git locally for command line workflow
- [ ] Create GitHub Organization (JustInTymeSports) when partners ready
- [ ] Transfer repo from jptymes personal to org account at that time
