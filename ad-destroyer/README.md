# AD DESTROYER

**THE INTERNET IS BROKEN. FIX IT WITH A HAMMER.**

An original, static-first Astro + TypeScript arcade game with practical internet safety tools. No backend, accounts, paid APIs, advertising SDKs, or external fonts.

## GitHub Pages test-site deployment

At the user's request this release is being added to the existing `andrejhalas/andrejhalas.github.io` test host, under `/ad-destroyer/`. Existing root, studio and privacy pages remain unchanged.

Target URL: https://andrejhalas.github.io/ad-destroyer/

The host publishes static files from its existing branch. The compiled application is in `ad-destroyer/`; `ad-destroyer-source.zip` contains the complete editable source, tests, lockfile and deployment documentation. Extract it to a separate working directory, then run:

```sh
npm ci
SITE_URL=https://andrejhalas.github.io SITE_BASE_PATH=/ad-destroyer npm run verify
```

Copy `dist/` into the host repository's `ad-destroyer/` directory and commit that directory only. Assets use `assets/` so Jekyll does not discard underscore-prefixed bundles. Do not replace host-root files. GitHub Pages ignores Cloudflare `_headers`; subdirectory robots.txt is not authoritative for the entire host. The sitemap and helper-page noindex still apply. The custom 404 is available in this subdirectory, but the host controls its global 404 response.

The standalone `.github/workflows/pages.yml` is provided for a future dedicated repository; it is not installed into the existing host's workflow directory. No new paid services or domains are used. This build uses the actual existing host origin and subdirectory for canonical, social and sitemap URLs.

## Release state

Production build, TypeScript diagnostics and all nine automated tests pass for the actual target origin and base path. Published successfully at https://andrejhalas.github.io/ad-destroyer/ (deployment commit `8c1182f33892453598e2ca7434e981604cb89dc2`, Pages run `38165619247`: success). Live Chrome smoke checks passed for all weapons, score updates, simulator and direct popup test. Physical-device audio, haptic and browser-policy acceptance remain manual checks.

## Included features

- `/`: six waves, original fictional ad targets, score, expiring combos, hammer strikes, press-and-hold chainsaw damage, laser cooldown and burns, bounded Canvas debris, synthesized sounds, reduced motion, optional vibration, pause, restart, and Web Share / clipboard / manual-copy fallback.
- Cookie Consent Monster: destroy three separate shields before the boss can take damage.
- Unskippable Video Ad: attacks only work during repeating green skip windows.
- `/fake-virus-popup/`: explicitly harmless fictional simulation, four inspectable scam tactics, hammer destruction, obvious exit, practical safety guidance, FAQ, and official browser help links.
- `/popup-blocker-test/`: one same-site `window.open()` attempt per user request; direct and six-second delayed tests; cancellation, close-window control, and conservative allowed / likely-blocked / inconclusive results.
- `/dark-pattern-examples/`: six original interactive examples, explanations, fair alternatives, and reversible destruction.
- `/privacy/`, a noindex test-window helper, and custom 404.
- Unique static titles/descriptions, canonical URLs, social PNG, Open Graph, WebSite JSON-LD, sitemap, robots.txt, navigation and internal links.
- Future sponsorship slot outside the arena, clearly labeled and inactive.
- GitHub CI workflow; dependency versions and lockfile pinned.

## Local setup

Use Node.js **24 LTS** and npm.

```bash
npm ci
npm run dev
```

Open the local address printed by Astro. Start the arcade with **Start smashing**. Select weapons with buttons or keys 1, 2, 3. Press and hold a target to use the chainsaw; keyboard users can strike with repeated Enter presses. Escape pauses/resumes a running game.

```bash
npm run verify
npm audit --audit-level=high
```

`verify` runs Astro/TypeScript checks, a fresh static build, and the automated tests. Tests need the freshly generated `dist/`. The default local build intentionally disallows crawling and marks pages `noindex`.

## Create the NEW GitHub repository

The desired account and name are `ahdigitallabs/ad-destroyer`. Do not reuse a different repository. From the extracted `ad-destroyer/` folder, with GitHub CLI authenticated as the intended account, restore the included committed history:

```bash
git clone ../ad-destroyer-history.bundle ad-destroyer-checkout
cd ad-destroyer-checkout
git remote remove origin
gh auth status
gh repo create ahdigitallabs/ad-destroyer --public --source . --remote origin --push
```

The bundle is beside this project folder in the release archive. If the requested repository name already exists, stop and review ownership and content; do not overwrite it. Public repository visibility supports free GitHub Pages hosting.

Alternatively create an **empty** repository through `https://github.com/new` with owner `ahdigitallabs` and name `ad-destroyer`. Do not initialize a README or license. Then push the restored local `main` branch:

```bash
git remote add origin https://github.com/ahdigitallabs/ad-destroyer.git
git push -u origin main
```

## Optional alternative: Cloudflare Pages Git integration

1. Sign in to the intended Cloudflare account. Go to Workers & Pages and choose a new **Pages** application connected to Git.
2. Authorize only the new `ahdigitallabs/ad-destroyer` repository. Select production branch `main`.
3. Use project name `ad-destroyer` if available. Framework preset: Astro. Root directory: repository root. Initial build command: `npm run build`. Output directory: `dist`. Set build environment `NODE_VERSION=24`.
4. The first build may use the safe localhost/noindex default solely to obtain the **actual assigned project URL**. Do not submit it to search engines or treat it as the release.
5. Copy the actual production project origin shown by Cloudflare into the production environment variable `SITE_URL`. Use the stable production origin, not a hash-specific preview URL. Set the build command to `npm run build:pages`.
6. Redeploy the same commit. The final build regenerates canonical URLs, social URLs, sitemap and robots for that actual `https://<assigned-project>.pages.dev` address. `build:pages` rejects missing, localhost, non-HTTPS, and non-Pages origins.
7. Visit all four MVP pages, confirm metadata and sitemap match the assigned URL, and complete the browser/device checks in `QA_REPORT.md` before announcing launch.

Use Cloudflare's included free tier; do not enable paid products or a custom domain. The requested hostname is not guaranteed until assigned by Cloudflare.

Official instructions: https://developers.cloudflare.com/pages/get-started/git-integration/

## Alternative: Wrangler Direct Upload

Choose this instead of Git integration only if you want manual deployments. A Direct Upload Pages project cannot later be converted to a Git-integrated project; Cloudflare requires a new project for that change.

On an authenticated local workstation:

```bash
npm ci
npx wrangler login
npx wrangler pages project create ad-destroyer --production-branch main
npx wrangler pages project list --json
```

Use the **actual production subdomain returned for the new project** as `SITE_URL`, then run:

```bash
# Replace this placeholder with the confirmed project origin.
export SITE_URL='https://ACTUAL-ASSIGNED-PROJECT.pages.dev'
npm run check
npm run build:pages
npm test
npx wrangler pages deploy dist --project-name ad-destroyer --branch main
```

If the project name is unavailable, choose a different NEW project name and update `--project-name` to it. Never deploy into an existing unrelated project. Wrangler receives credentials through its own login flow; do not paste tokens into source files or chat.

Official instructions: https://developers.cloudflare.com/pages/get-started/direct-upload/

## Analytics

`src/scripts/telemetry.ts` emits the requested events using `window.dispatchEvent(new CustomEvent('ad-destroyer:event', ...))`:

`game_start`, `weapon_selected`, `ad_destroyed`, `boss_defeated`, `game_completed`, `score_shared`, `simulator_started`, `popup_test_started`, `popup_test_completed`.

They are **local hooks, not a configured remote collector**. There are no identifiers, cookies, personal data fields, or network requests from this module. Event properties are limited to game/test enums and numeric score.

Optional Cloudflare Web Analytics page/performance reporting: set `PUBLIC_CF_ANALYTICS_TOKEN` to your site's public beacon token and rebuild. This token is not an API secret. Leave it empty to keep the beacon disabled. If Cloudflare automatically injects a beacon, do not also set this variable: avoid duplicate reporting.

Cloudflare Web Analytics is separate from the local game events; its beacon does not ingest these custom events through this implementation. To add aggregate game-event reporting later, choose a documented collector, minimize data, update the privacy page, and assess the actual audience's disclosure/consent requirements before enabling it. Hosting request logs are handled by the hosting provider independently of the game hooks.

## Architecture and constraints

- Astro generates all content and educational explanations as HTML. Canvas contains decorative particles only.
- The arcade engine is dynamically imported on the first Start click. Informational pages load only their small interaction script.
- Animation uses one requestAnimationFrame loop while playing. Pausing, finishing and hidden-tab handling stop it. Debris is capped at 150 particles; Canvas pixel ratio is capped at 2.
- The elapsed game timer pauses while hidden. This is casual play, not a competitive anti-cheat system.
- Audio begins only after user interaction and explicit unmute. Vibration is optional and may be unsupported.
- No personal data entry, device scan, permission prompts, external downloads, paid calls, real ads, or transactions are part of the demonstrations.
- WebSite structured data is used; no invented reviews, ratings, or unsupported rich-result claims are added.

See **QA_REPORT.md** for verified checks, verification limits, and next steps.
