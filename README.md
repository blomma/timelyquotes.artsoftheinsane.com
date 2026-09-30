# Timely Quote promotional website

Static promotional site for [Timely Quote](https://apps.apple.com/app/id6466886308), following the visual structure of `vilar.artsoftheinsane.com` while using Timely Quote's own colors, icon, screenshots, features, and privacy language.

## Constraints

- The shipped page contains HTML and CSS only. There is no client-side JavaScript.
- The page uses system fonts and local, compressed images; it makes no font, image, analytics, or tracking requests to third parties.
- `index.html` and `style.css` are the editable sources. `public/` holds static assets. `docs/` is the generated GitHub Pages artifact.
- `public/CNAME` configures `timelyquotes.artsoftheinsane.com`.

## Commands

```sh
npm install
npm run check
npm run build
npm run dev
```

`npm run build` writes the deployable site to `docs/`.

## Verified product facts

Verified against `../vittra.literaturetime` on 30 September 2026:

- The quote dataset contains **13,530 records across 1,406 distinct `time` values**. These totals were computed from `Quotes/literatureTimes.json` with `jq`, and match the shipped store: `select count(*), count(distinct ZTIME) from ZLITERATURETIME` on `Quotes/literatureTimes.store` returns `13530|1406`.
- The app highlights the time phrase, uses readable adaptive line lengths, and supplies VoiceOver content in `vittra.literaturetime/Views/LiteratureTimeView.swift:66-104`.
- Pull-to-refresh is implemented in `vittra.literaturetime/Views/LiteratureTimeView.swift:136-138`. Optional minute-boundary auto-refresh is started in `vittra.literaturetime/Views/LiteratureTimeView.swift:139-150` and runs in `LiteratureTimeFeature/Sources/LiteratureTimeFeature/LiteratureTimeModel.swift:78-105`.
- Share, copy, refresh, and Project Gutenberg actions are implemented in `vittra.literaturetime/Views/QuoteContextMenu.swift:22-42`.
- The library is loaded from a bundled, read-only SwiftData store in `Providers/Sources/Providers/ModelProvider.swift:9-28`.
- The iPhone and iPad device families are both enabled for the app target in `vittra.literaturetime.xcodeproj/project.pbxproj:362` (Debug) and `:401` (Release).
- The tip jar offers three consumable tips (`TipJarFeature/Sources/TipJarFeature/Tip.swift`, `TipProductID.all`) sold through StoreKit in `TipJarFeature/Sources/TipJarFeature/StoreKitTipStore.swift:22-55`. Prices are the App Store's localized `displayPrice`, so the site names no prices.
- The app stores nothing about tips itself. The "thank you" shown to supporters comes from StoreKit's purchase history via `Transaction.all` in `StoreKitTipStore.swift:57-67`. That depends on `SKIncludeConsumableInAppPurchaseHistory` being `true` in `vittra.literaturetime/Info.plist:7-8`.
- The Tip Jar loads the tips from the App Store when it opens (`vittra.literaturetime/Views/Settings/TipJarView.swift:46-48`). It states in the app that tips are optional and unlock nothing (`TipJarView.swift:20`).
- Settings links to the App Store review page as "Rate Timely Quote" (`vittra.literaturetime/Views/Settings/SettingsAppSection.swift:12-14`, URL in `ExternalLink.swift:11`). The app never shows a rating prompt on its own.
- The app's privacy statement says it does not collect or process personal information in `PRIVACY.md:1`. A source scan found no networking, analytics, advertising, or tracking APIs in the app's Swift and package manifests.
- The App Store listing at `https://apps.apple.com/app/id6466886308` identifies the app as free and available for iPhone and iPad.

## Asset provenance

- `icon.webp`, `favicon.png`, `apple-touch-icon.png`, and `og-image.png` derive from `../vittra.literaturetime/Assets/appicon_1024.png`.
- `shot-clock.webp`, `shot-settings.webp`, `shot-actions.webp`, and `shot-tablet.webp` are compressed, resized exports of the deterministic UI-test captures under `../vittra.literaturetime/screenshots/raw/`. The raw files have generated names; `manifest.json` in each device folder maps them to screen names through `suggestedHumanReadableName`.
- All four were regenerated on 30 September 2026 (evening) after the App Store screenshot plan was rebuilt; see `../vittra.literaturetime/ASO.md`. Settings now shows the Tip Jar and "Rate Timely Quote" rows with automatic refresh switched on. The quote menu now reads "View book on Project Gutenberg" and "Copy Project Gutenberg link".
- Mapping: iPhone `01_LiteraryClock` → `shot-clock`, `05_AutoRefresh` → `shot-settings`, `03_ReadTheBook` → `shot-actions`, resized from 1320×2868 to 640×1391. iPad `01_LiteraryClock` → `shot-tablet`, resized from 2064×2752 to 768×1024. Each is resized with `magick … -resize WxH!` and encoded with `cwebp -q 85 -m 6`. `shot-clock` and `shot-tablet` came out byte-identical to the previous files, since those screens didn't change.
- The WebP screenshots are 13–41 KB each. The Open Graph image is a local, indexed-color 1200×630 PNG.

## Validation record

Last run 30 September 2026, after adding the tip jar section and the new screenshots:

- Prettier check passed.
- Vite production build passed and produced no JavaScript bundle.
- `npm audit` reported zero vulnerabilities.
- All image dimensions and HTML width/height attributes were checked against the generated files.
- The built page was rendered with JavaScript disabled in local WebKit at 1440×1050 and 390×844 viewport sizes; the hero, responsive navigation (now three links), device composition, tip jar section, CTA, and summary strip rendered correctly at both sizes.
