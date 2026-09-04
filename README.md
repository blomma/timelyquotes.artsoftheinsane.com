# Timely Quote promotional website

Static promotional site for [Timely Quote](https://github.com/blomma/vittra.literaturetime), following the visual structure of `vilar.artsoftheinsane.com` while using Timely Quote's own colors, icon, screenshots, features, and privacy language.

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

Verified against `../vittra.literaturetime` on 4 September 2026:

- The quote dataset contains **13,521 records across 1,406 distinct `time` values**. These totals were computed directly from `Quotes/literatureTimes.json` with `jq`.
- The app highlights the time phrase, uses readable adaptive line lengths, and supplies VoiceOver content in `vittra.literaturetime/Views/LiteratureTimeView.swift:52-101`.
- Pull-to-refresh and optional minute-boundary auto-refresh are implemented in `vittra.literaturetime/Views/LiteratureTimeView.swift:126-180`.
- Share, copy, refresh, and Project Gutenberg actions are implemented in `vittra.literaturetime/Views/QuoteContextMenu.swift:17-41`.
- The library is loaded from a bundled, read-only SwiftData store in `Providers/Sources/Providers/ModelProvider.swift:10-24`.
- The iPhone and iPad device families are both enabled in `vittra.literaturetime.xcodeproj/project.pbxproj:373-394`.
- The app's privacy statement says it does not collect or process personal information in `PRIVACY.md:1`. A source scan found no networking, analytics, advertising, or tracking APIs in the app's Swift and package manifests.
- The App Store listing at `https://apps.apple.com/app/id6466886308` identifies the app as free and available for iPhone and iPad.

## Asset provenance

- `icon.webp`, `favicon.png`, `apple-touch-icon.png`, and `og-image.png` derive from `../vittra.literaturetime/Assets/appicon_1024.png`.
- `shot-clock.webp`, `shot-settings.webp`, `shot-actions.webp`, and `shot-tablet.webp` are compressed, resized exports of the deterministic UI-test captures under `../vittra.literaturetime/screenshots/raw/`.
- The WebP screenshots are 12–36 KB each. The Open Graph image is a local, indexed-color 1200×630 PNG.

## Validation record

- Prettier check passed.
- Vite production build passed and produced no JavaScript bundle.
- `npm audit` reported zero vulnerabilities.
- All image dimensions and HTML width/height attributes were checked against the generated files.
- The built page was rendered with JavaScript disabled in local WebKit at 1440×1050 and 390×844 viewport sizes; the hero, responsive navigation, device composition, CTA, and summary strip rendered correctly at both sizes.
