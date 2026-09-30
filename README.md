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
- The app highlights the time phrase, uses readable adaptive line lengths, and supplies VoiceOver content in `vittra.literaturetime/Views/LiteratureTimeView.swift:59-98`.
- Pull-to-refresh is implemented in `vittra.literaturetime/Views/LiteratureTimeView.swift:130-132`. Optional minute-boundary auto-refresh is started in `vittra.literaturetime/Views/LiteratureTimeView.swift:133-144` and runs in `LiteratureTimeFeature/Sources/LiteratureTimeFeature/LiteratureTimeModel.swift:78-105`.
- Share, copy, refresh, and Project Gutenberg actions are implemented in `vittra.literaturetime/Views/QuoteContextMenu.swift:22-42`.
- The library is loaded from a bundled, read-only SwiftData store in `Providers/Sources/Providers/ModelProvider.swift:9-28`.
- The iPhone and iPad device families are both enabled for the app target in `vittra.literaturetime.xcodeproj/project.pbxproj:355` (Debug) and `:394` (Release).
- The app's privacy statement says it does not collect or process personal information in `PRIVACY.md:1`. A source scan found no networking, analytics, advertising, or tracking APIs in the app's Swift and package manifests.
- The App Store listing at `https://apps.apple.com/app/id6466886308` identifies the app as free and available for iPhone and iPad.

## Asset provenance

- `icon.webp`, `favicon.png`, `apple-touch-icon.png`, and `og-image.png` derive from `../vittra.literaturetime/Assets/appicon_1024.png`.
- `shot-clock.webp`, `shot-settings.webp`, `shot-actions.webp`, and `shot-tablet.webp` are compressed, resized exports of the deterministic UI-test captures under `../vittra.literaturetime/screenshots/raw/`.
- All four were regenerated on 30 September 2026 from that day's captures, so they show the current app: the Liquid Glass quote-actions button and Settings without the "Source (GitHub)" row. iPhone captures (`01_LiteraryClock` → `shot-clock`, `02_Personalize` → `shot-settings`, `04_ReadTheBook` → `shot-actions`) are resized from 1320×2868 to 640×1391, and the iPad `01_LiteraryClock` capture (→ `shot-tablet`) from 2064×2752 to 768×1024, with `magick … -resize WxH!`, then encoded with `cwebp -q 85 -m 6`.
- The WebP screenshots are 13–41 KB each. The Open Graph image is a local, indexed-color 1200×630 PNG.

## Validation record

- Prettier check passed.
- Vite production build passed and produced no JavaScript bundle.
- `npm audit` reported zero vulnerabilities.
- All image dimensions and HTML width/height attributes were checked against the generated files.
- The built page was rendered with JavaScript disabled in local WebKit at 1440×1050 and 390×844 viewport sizes; the hero, responsive navigation, device composition, CTA, and summary strip rendered correctly at both sizes.
