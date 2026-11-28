<div align="center">

# Ibili

**Bilibili on iPad, redesigned from scratch.**

**[← 中文](README.md)**　·　English　·　by **Xi/ElioXBlaze**　·　QQ group **1134860332**

**Current version 4.1.5** · MIT License · single-file userscript

</div>

Desktop Bilibili on the web has every feature and a real keyboard. The mobile app has gestures that feel right and an interface that looks right. **Ibili joins the two** — it keeps the whole web feature set, then gives it a modern interface and app-grade touch gestures.

Version 4.0 completed a full core swap: the UI runtime now runs on a **single-file iPadOS Safari transpilation of BewlyCat 1.8.5** (the community successor to the archived BewlyBewly), while the player layer and the merge layer stay as they were. One file, one install, and a language picker the first time you open it.

---

## Decide in 30 seconds

| | | |
|---|---|---|
| **41** speed steps, 0.0312×–32× | **11** UI languages | **30** shortcuts |
| **No system fullscreen**, danmaku intact | **1 file**, no build, no deps | **0** telemetry |

Settings are not a floating panel — they **live inside the site's own settings window**, with a search box that finds every setting. Videos you dislike disappear in one tap. Videos you want are always within reach.

---

## The good stuff, first

### ① Playback: full keyboard, full speed range, danmaku intact

Autoplay tries with sound first, falls back to muted only when the browser refuses, and quietly restores audio on your first gesture. Volume is remembered. **41 extended speed steps** (full range on keyboard, touch hold capped at 6×), with hold, lock, step-through and memory.

`F` forwards to **Bilibili's own web-fullscreen button only**. System fullscreen / AVKit paths are intercepted and redirected, because that layer drops danmaku, the control bar and every long-press gesture. `Shift+F` adjusts picture fill: crop black bars in landscape, keep the whole frame (and faces) in portrait.

Background playback and PiP follow capability detection: enabled when supported, exited automatically when you return, media metadata wired into the system Control Center. What cannot be done is reported honestly, never faked.

### ② Touch: feels like an app, not a page

All gestures live in the web layer — the video is never handed to the native player: long-press for temporary 2×, hold to lock, slide up/down while holding to step or unlock, left half for visual brightness, right half for page volume, horizontal swipes yield to Bilibili's native seek. The 0–100% glass HUD inherits the theme, blur and opacity of the redesign layer. Since 4.0 the center-screen gesture HUD is gone — only the two side bars remain, so nothing covers the picture.

### ③ You control the feed

Bottom-right **×** = one-tap "Not interested": it runs the redesign layer's dislike entry, reports the official dislike, and the card disappears on the spot.
Bottom-left **＋** = your local blocklist, resolved by uploader name (never stores "unknown uploader"), and **only actually hides cards when Study Mode is on**. Two buttons, one visual language, two separate jobs.

Plus `b` one-tap triple (auto-substitutes like/favorite when coins run out), `g` Study Mode, and `r` refresh that **verifies the cards actually changed** before reporting success. The factory baseline ships 15 checkable blocked zones.

### ④ A full redesign — settings you can search

Home, search, zones, dynamics, spaces, Watch Later and favorites are all re-laid-out: top bar and Dock, card grid, wallpaper and glass, Search Page Mode (large logo + large search bar + 22-娘). Theme color defaults to `#22c55e`; light and dark modes included.

Ibili's settings are **merged into the site's native settings window**, organized as a three-level information architecture: 7 top-level categories (General / Playback / Pages / Appearance / Interaction / Content / About), second levels mounted on the native sidebar, and a centered "Find settings" search box on top — **it searches every setting, results really navigate there, breadcrumbs stay in sync**. After a category switch or a Vue rebuild the index rescans automatically; no reload needed.

### ⑤ Eleven languages, asked on first launch

简体中文 · 繁體中文（香港）· 繁體中文（台灣）· English · 日本語 · 한국어 · Español · ไทย · Tiếng Việt · Bahasa Indonesia · Русский

First run: hello carousel → language picker → a one-time support dialog → never prompted again. Change it any time in settings; the page reloads once and brings the settings window back. Settings text, first-run flow and the engineering menu all share one dictionary.

> This layer covers Ibili's and the redesign layer's interface text only. Bilibili's own UI language and video titles / uploader names / comments are content owned by Bilibili — the script does not translate or alter them. It only writes language preference cookies and `<html lang>`.

### ⑥ Clean direct links and frame capture

On any playback page, Ibili lists the **watermark-free MP4 direct links** of the current video (read-only, only streams the page is allowed to play; Stay's download manager takes over first), and `j` captures a frame (with a canvas-taint probe — if the canvas is untouchable, it says so instead of failing silently; max side 1920).

---

## Install

1. Install **Stay** from the App Store and enable it in Safari extensions;
2. Stay → Userscripts → `+` → import `Ibili.user.js` via URL / file / paste, then **make sure the script switch is on**;
3. Safari address bar → "Size / aA" → **Request Desktop Website**, keep `www.bilibili.com`;
4. Reload Bilibili. The first run asks you to pick a language.

Manual download (paste into Stay's URL import):

```
https://raw.githubusercontent.com/ElioXBlaze/Ibili/main/Ibili.user.js
```

Metadata: `@run-at document-start`, 11 `@match` patterns (search / messages / space / member / music subdomains included), 10 `@connect`, 11 `GM_*` grants. Missing Stay APIs degrade gracefully instead of white-screening.

> **No auto-update**: the script declares neither `@updateURL` nor `@downloadURL`, so Stay will not check for new versions. Re-import or paste over it to upgrade; your settings and language choice are kept.

`m.bilibili.com` only gets partial functionality and desktop browsers are untested — this is built for the **iPad desktop web version**.

---

## Shortcut reference

**30** factory defaults, all editable in Settings → Shortcut remapping, plus a "Shortcut exclusivity" switch (window capture + `stopImmediatePropagation`, so other scripts on the page cannot fire on the same key); the 22 official player actions are folded into the same key system — remapping, conflict overview and one-tap avoidance share a single source of truth.

| Key | Action | Key | Action |
|---|---|---|---|
| `Space` | Play / pause | `←` / `→` | Seek back / forward |
| `↑` / `↓` | Volume up / down | `m` | Mute |
| `-` / `=` | Previous / next part | `,` | Refresh feed |
| `f` | Web fullscreen | `Shift+F` | Picture fill toggle |
| `Shift+R` | Fill reset | `t` | Wide mode |
| `[` / `]` | Speed down / up one step | `Shift+!` / `Shift+@` | Speed preset 1 / 2 |
| `d` | Danmaku toggle | `i` | Danmaku input / preset |
| `s` | Native search | `Shift+S` | Zero-nav search overlay |
| `b` | One-tap triple (confirm / fallback) | `r` | One-tap triple (official action) |
| `q` | Like | `w` | Coin |
| `e` | Favorite | `g` | Follow |
| `c` | Frame capture | `p` | Mini / PiP window |
| `;` | Study Mode | | |

The `Shift+S` overlay carries suggestions, hot searches and category navigation with zero navigation; `s` hands the cursor to Bilibili's own search box. Triple-tap fullscreen, keyboard volume bar and smooth brightness each have a one-tap switch under "Gestures / Playback & volume", and the smooth mode can revert to the legacy feel at any time.

---

## Full feature list

**Playback** — autoplay (sound first → muted on refusal → unmute on first gesture), remembered volume, 41 speed steps, remembered rate, temporary 2× on long-press and cancel, optional pitch preservation, background playback and PiP (capability-detected, auto-exit on return, MediaSession metadata, prewarm), watermark-free MP4 direct links (read-only, GM_download first), `j` frame capture (canvas taint probe, max side 1920).

**Touch** — hold-to-lock / slide-up stepping / slide-down unlock, left brightness (0–100%) and right volume, glass HUD, horizontal swipe yielding to native seek, rate lock, 160ms coalescing, 340ms hold threshold, 280ms / 10s / 44px touch parameters, all adjustable; the bottom-right 140px is reserved for iPadOS window-resize corner gestures.

**Search** — `s` native search box toggle (falls back to the overlay when no native box exists), `Shift+S` overlay (suggestions, hot searches, categories, zero navigation), a search guard that does not hijack official submissions; the overlay inherits the same design variables.

**Feed control** — one-tap triple, Study Mode, 15 default blocked zones and an uploader-mid blocklist, a zone entry panel (19 top-level zones with sub-zone mapping), verified refresh, bottom-right × official dislike + silent report, bottom-left ＋ local list.

**IP location** — the `__BP_IP__` module bridges the host's official IP-location info and its display toggle (since 4.1.5), with a dedicated `ip` settings card under Feed control and 11-language texts.

**Interface** — full redesign, wallpaper and mask (Rocky Mountains by default, 60% mask), light / dark modes, theme color `#22c55e`, right Dock, Search Page Mode (large logo + large search bar + 22-娘), adjustable glass and opacity, secondary navigation forced visible + unified "Level › Sub-level" breadcrumbs, eleven UI languages, first-run flow and support dialog (donation codes embedded in the script, no external image host).

**Engineering & data** — Stay script-menu commands registered synchronously at document-start (root-fixes the "no registered menu items" popup): one-tap self-checks generate a unified diagnostic log and **copy it to the clipboard** (all / touch / autoplay / refresh / volume / background PiP / login state / languages / danmaku / theme / search), Force-mount Dock, Factory reset, Export / Import all settings (export **auto-enumerates every storage key** via `GM_listValues` since 4.0.6 — one JSON, auto-copied and downloaded), re-pick language / replay the welcome flow.

**On-device self-checks** (Safari / Stay console, all read-only)

```js
__BP_UI_API__.deviceCheck()        // version, language, buttons, request bridge, Dock, wallpaper
__BP_UI_API__.xhrBridge()          // which channel requests actually took
__BP_UI_API__.logoZone()           // zone entry state
__BP_UI_API__.wallpaperViewport()  // wallpaper pinning state
__BP_I18N_AUDIT__()                // walks the whole page, lists uncovered visible text
```

---

## How it is built

The repository ships **one finished `Ibili.user.js`**. It embeds the BewlyCat 1.8.5 UI runtime (the community-maintained successor to BewlyBewly, transpiled for iPadOS Safari as a single file, including the Vue runtime and all styles), the BiliPad player layer, and a merge layer that puts both complete scripts on **one settings store, one menu, one lifecycle** — not two parallel sets of listeners.

> There is **no `src/` and no build script** in the repo. The "sources" mentioned in the file header describe logical lineage, not a reproducible build chain. Edit the shipped file directly and run the regression suite.

The hard parts were all iPad Safari specifics:

- **Shadow DOM** — the redesign layer mounts its Vue app inside `#bewly`'s ShadowRoot, which plain `document.querySelector` cannot reach. Injection, styles and click targeting walk shadowRoots individually; events use `composedPath()` to beat retargeting.
- **Request bridge** — Stay's `GM_xmlhttpRequest` loses login cookies cross-site to `api.bilibili.com`, so Watch Later / favorites falsely reported "not logged in". Now the `window.fetch` layer is the single choke point: reserved headers stripped, same-site rewrites for writes, missing csrf filled with `bili_jct` — every script's requests pass through it.
- **Settings search** — the settings index is built at runtime from real IA paths; hidden native rows never enter it; clicking a result really navigates and syncs the breadcrumb. The index rescans after Vue rebuilds, one search box = one visible result area.
- **Wallpaper viewport** — Safari's layout and visual viewports differ while toolbars animate. The wallpaper layer is pinned with `100dvh`, `transform:none` and `background-position:center bottom`, rescanned via `visualViewport`.
- **Route healing** — `?page=` routes plus Safari bfcache could blank the page (or drop the whole script) on Back; `popstate` / `pageshow` now heal it, with a single reload only when the redesign layer is genuinely gone.
- **Factory baseline** — one JSON (schema 39) is the single source of truth for first load, factory reset and "restore defaults". On upgrade, seeding steps aside so custom keys, theme and language are never overwritten.

**Verification**: Chromium-simulation regression suites plus on-device self-check entries all green; iPad Safari + Stay is iterated continuously with feedback and screenshots from users. **No claim of full developer-side on-device coverage.**

---

## Known limits

- **System volume is off-limits to web pages** on iOS / iPadOS — hardware keys and Control Center own it. The right-half bar adjusts the page volume layer.
- **True edge-to-edge is impossible** — Safari's address bar, tab bar and home indicator are system chrome. A portrait video cannot be both complete and edge-to-edge.
- **Built for the iPad desktop web version** — `m.bilibili.com` gets partial functionality, desktop browsers are untested.
- **Automatic PiP** — Apple requires `AVPlayerViewController` for gesture-less PiP; the web layer has no such switch. Unsupported cases are reported honestly, never faked.
- **Language boundary** — Bilibili's own UI language and video titles / uploader names / comments are not decided by the script; it writes preferences only and never rewrites URL language segments.
- **Do not run two redesign scripts** — the official BewlyBewly / BewlyCat or another home-redesign script will fight over the same DOM. Keep one.
- **The "Open in the Bilibili App" banner at the top of every shot** is Safari's Smart App Banner, drawn by the system from the page meta. The script cannot hide it.

### FAQ

**Nothing happens after install?** Check Request Desktop Website, `www.bilibili.com`, and the Stay script switch; then run `__BP_UI_API__.deviceCheck()` and look at `fetchPatched` and `shadowRoots`.

**Dock vanished?** Stay script menu → Force-mount Dock. If it is still gone, check whether the URL carries a language segment like `/ja/` (old versions did that; current ones do not).

**Back to a fresh install?** Stay script menu → Factory reset wipes GM / localStorage / sessionStorage / language cookies / URL language segments and replays the first-run flow. **It erases custom settings** — export all settings first.

**Will upgrading re-show the language / support dialogs?** No. `langDone` / `donateDone` persist; only clearing script data or a factory reset replays them.

---

## Changelog

Full history: [Releases](https://github.com/ElioXBlaze/Ibili/releases). 3.x covered the merge, settings integration, languages, touch and on-device structural fixes; 4.0 swapped the core to BewlyCat. Highlights:

- **4.1.5** — **IP location**: the `__BP_IP__` module bridges the host's official IP-location info and its display toggle, with a dedicated `ip` settings card under Content governance and 11-language texts; playback-rate protection against fighting the player's native rate (`__IBILI_NATIVE_RATE__` 1.5-second truth window, native wins); danmaku toggle self-heals (previous-state record + retry on failure).
- **4.1.4** — **keyboard system convergence**: 22 official player actions folded into Ibili commands sharing one source of truth with native keys; conflict overview + one-tap avoidance, key guard (BP_KEY414) prevents double-firing; the two search-page switches merged into their feature card; factory defaults taken from a user-confirmed export snapshot.
- **4.1.3** — settings pages homed: the danmaku page keeps only danmaku items, 10 danmaku presets merged into card 0; triple-tap fullscreen / keyboard volume bar / smooth brightness moved to "Gestures" and "Playback & volume".
- **4.1.2** — danmaku presets / triple-tap fullscreen / keyboard volume bar / auto-pause added; smooth brightness: same-frame merged writes + removal of the 0.01 quantization ladder, with a switch to revert.
- **4.1.1** — portrait adaptation: portrait orientation renders "video width = screen width" with letterboxing top/bottom, no longer judged by landscape ratio alone.
- **4.1.0** — **purely Ibili**: version and naming globally synced to the single `__IBILI_VER__` source of truth, diagnostics detail restored; branding, identity, console prefixes and `current_contributors` all consolidated to Ibili (by Xi/ElioXBlaze); third-party credits, manifests and license texts at the tail of the script were removed by author decision — the script belongs to Ibili alone.
- **4.0.7** — unified version source of truth: every version readout now derives from a single `__IBILI_VER__` (one line per release; display, bookkeeping and backups sync automatically); the version-reminder dialog drops its Release-style layout and centers all elements; the help bar is removed — backup/restore lives only on the About page.
- **4.0.6** — official release (three batches of verifiable fixes folded in): Stay menu registration root-fixed, export auto-enumerates all storage keys, autoplay gesture finalized, About-page donation images restored.
- **4.0.5** — settings-page UI stacking root-fixed: nine legacy injection functions short-circuit when V5 is active; bewlycat leftover settings entries and the duplicate bottom-right icon removed; one search box in the settings window with results on real IA paths; 14 secondary pages forced visible, breadcrumbs unified to "Level › Sub-level"; center gesture HUD removed, only left-brightness / right-volume bars remain; the "Engineering" settings page deleted, entries live only in the Stay userscript menu.
- **4.0.0** — **core swap**: UI runtime switched to a single-file iPadOS Safari transpilation of BewlyCat 1.8.5, replacing BewlyBewly v0.41.1; settings rebuilt as a three-level IA (7 top categories / second level on the native sidebar / centered "Find settings" box); UI languages expanded from 9 to 11 (Korean, Thai, Vietnamese, Indonesian added).
- **3.1.0** — viewport convergence: one `--ibili-vh` source of truth, root-fixes recurring bottom white/black strips, ghost text and residue; adds `viewportState()`.
- **3.0.22** — bottom-right × becomes a real one-tap "Not interested"; uploader names read from redesign cards.
- **3.0.20** — five legacy panel render functions deleted; settings fully merged into the native window.
- **3.0.13** — factory baseline lands: one state for first load / factory reset / restore defaults.

---

## Feedback

QQ group **1134860332**. Invite links may expire; searching the number always works. A screenshot plus `__BP_UI_API__.deviceCheck()` output makes bug reports much faster.

---

## Credits

- [BewlyCat](https://github.com/keleus/BewlyCat) — the direct source of the UI runtime swapped in at 4.0 (1.8.5, single-file iPadOS Safari transpilation). From 4.1.0 the script no longer carries upstream credits or license texts; the lineage note lives here.
- [BewlyBewly](https://github.com/BewlyBewly/BewlyBewly) — the origin of the redesign language and interaction patterns, MIT, archived (last release v0.41.1).
- [Bilibili-Evolved](https://github.com/the1812/Bilibili-Evolved) — componentization inspiration only; no code from it is included and no license claim is made about it.
- Everyone who left B-station script notes on Greasy Fork.

---

## Disclaimer

A personal, self-use browsing-experience script, unrelated to Bilibili officially. It does not bypass paid content, does not crack anything, and collects or uploads no usage data; network requests only load page resources and call Bilibili's own endpoints. Use at your own risk and follow the platform terms.

## License

[MIT](LICENSE). The script itself no longer embeds a third-party license manifest — since 4.1.0 the tail of the script keeps only the Ibili identity and repository URL; for lineage history see the Credits above and this repository's commit history.
