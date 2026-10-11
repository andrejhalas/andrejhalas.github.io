# AD DESTROYER — QA report

Date: 2026-10-11. Scope: implemented MVP source and locally generated static output.

## Status

**Production build and all nine automated checks pass for `https://andrejhalas.github.io/ad-destroyer/`.** At the user's request, publication targets the existing GitHub Pages test host via an additive subdirectory. No existing root, studio or privacy files are changed. Live Chrome smoke checks pass; physical-device acceptance remains pending.

## Executed checks

| Check | Result | Evidence / coverage |
| --- | --- | --- |
| Astro and TypeScript diagnostics | PASS | `npm run check`: zero errors, warnings and hints |
| Static production build | PASS | `npm run build`: seven HTML pages plus sitemap and robots generated |
| Automated test suite | PASS | Nine tests; zero failures |
| Dependency audit | PASS | `npm audit --audit-level=high`: zero vulnerabilities after upgrading to Astro 7.3.8 |
| Hammer | PASS, DOM simulation | Touch-type pointer strike, keyboard click, health loss and target destruction |
| Chainsaw | PASS, DOM simulation | Held pointer produces damage across animation ticks; pointercancel releases hold |
| Laser | PASS, logic/DOM simulation | Stronger damage and cooldown preventing immediate repeat attacks |
| Cookie Consent Monster | PASS | Shielded boss resists attacks; three distinct shield buttons unlock damage |
| Unskippable Video Ad | PASS | Damage rejected outside skip window; accepted during green phase |
| Full game lifecycle | PASS | All six waves, both bosses, completion, time-up, pause/resume and restart |
| Score sharing | PASS, API mocks | Web Share success, clipboard success, denied clipboard manual-copy fallback |
| Reduced motion | PASS, logic/DOM simulation | Debris suppressed with reduced-motion preference; CSS disables animations and transitions |
| Virus simulator | PASS | Inspect claim, destroy warning, exit and restart restore original state |
| Popup result classification | PASS, API mocks | Usable window, null handle, immediately closed handle and thrown exception |
| Popup controls | PASS, DOM/API mocks | No unsolicited opening, direct request, delayed scheduling, cancellation, delayed callback, close control |
| Dark patterns | PASS | Six cards, fair-design toggle, destruction/reset, misleading-download response, scarcity change |
| Static SEO | PASS | Five content pages have unique title/description, one H1, canonical, OG URL, valid local assets, WebSite JSON-LD |
| Sitemap and robots | PASS | Five intended content URLs; helper excluded and marked noindex; local build safely disallows crawling |
| Links/navigation | PASS, static validation | All internal links and referenced local assets resolve in build output |
| Accessibility basics | PASS, static/DOM checks | Native buttons with names, main/nav landmarks, skip link, visible focus styling, status feedback and keyboard actions |
| Ad separation | PASS, source/output review | Original fictional targets only; no ad-network script; future sponsorship outside arena |
| Public access architecture | PASS, source review | Static pages; no authentication, backend, database or account wall |

## Method and honest limits

The interaction tests use Node's test runner and Happy DOM with controlled PointerEvents, animation ticks and popup/share API mocks. This exercises the actual TypeScript event handlers and generated HTML, but **is not a real browser rendering, popup-policy, or physical touchscreen test**.

The managed environment did not expose the required browser-control capability. No browser was installed and no substitute preview/browser path was used. Accordingly, visual layout, real console behavior, sound synthesis, haptics, true Safari/Chrome popup policy, physical touch capture and real browser accessibility are **unverified**. Those items must not be represented as passed.

Bundle checks enforce fewer than 50 KB of uncompressed application JavaScript and fewer than 500 KB of static output. Actual build is well below those limits. These are file-size checks, **not measured Core Web Vitals or Lighthouse scores**. No traffic estimates, ranking guarantees, or keyword search volumes were invented.

Browser-security content links were selected from official Google, Apple, Mozilla, and Microsoft guidance. Product safety rules were reviewed against the actual implementation: no permissions, personal inputs, downloads, payments, remote access requests, or OS impersonation.

## Release acceptance after integrations become available

1. Publish the compiled subdirectory and source archive to the existing test host authorized by the user.
2. Confirm publication at https://andrejhalas.github.io/ad-destroyer/ and check live canonical, OG and sitemap URLs.
3. On Chrome/Firefox/Edge desktop, play through all six waves with each weapon, use keyboard-only navigation, mute/unmute, pause, restart and share. Check console for uncaught errors.
4. On real Android Chrome and iPhone Safari, inspect at small widths, tap the hammer and laser, hold/cancel the chainsaw, scroll outside targets, rotate the phone and repeat boss encounters.
5. Run direct and delayed popup tests under default blocking, a site exception, and an in-app browser. Verify conservative wording matches observed handles; verify cancel and close controls.
6. Enable reduced motion on the device; verify no shake, beam animation, debris or continuous saw jitter. Confirm all explanatory pages remain useful with JavaScript disabled.
7. Check mobile layout for clipping and overlapping targets, keyboard focus continuity, text contrast, screen-reader announcements, and actual sound/haptic behavior.
8. Measure Lighthouse or field Core Web Vitals on the public URL. Inspect cache/header behavior and direct navigation to all routes.

## Known limitations and next steps

- GitHub Pages deployment succeeded; primary deployment commit `8c1182f33892453598e2ca7434e981604cb89dc2`, successful Pages run `38165619247`.
- Physical-device acceptance and exhaustive cross-browser QA remain open. Live Chrome smoke checks are recorded below.
- No remote custom-event analytics collector; all nine requested event names are implemented as browser-local hooks. Optional Cloudflare visit/performance analytics is disabled by default.
- No saved scores, leaderboard, anti-cheat, or daily challenges. Restart/reload resets session state.
- Popup tests are intentionally narrow and cannot certify security, ad blocking, or notification blocking.
- Weapons use lightweight synthesized sounds and browser-native symbols; haptics vary by platform.
- The build uses the existing GitHub Pages host. No custom domain has been purchased or connected.

The next priority is deployment and real-device acceptance, followed by measured performance and user feedback. Content expansion should follow observed search demand rather than filler generation.

## GitHub Pages test-host build

`SITE_URL=https://andrejhalas.github.io SITE_BASE_PATH=/ad-destroyer npm run verify` passed: zero diagnostics, successful production build, nine passing tests. Assets use a Jekyll-compatible directory. The deployment adds only the application subdirectory and source archive. GitHub Pages ignores Cloudflare `_headers`; subdirectory robots.txt cannot control account-root crawler policy.

## Live Chrome smoke verification

URL: https://andrejhalas.github.io/ad-destroyer/

- Pages deployment run 38165619247 completed successfully.
- Start dynamically loaded the game; hammer reduced target health 62→28 and a second strike destroyed it, awarding 100 points.
- Held chainsaw reduced a second target's health 62→35. Selecting laser and firing destroyed a third target, raising score to 200.
- Navigation to popup test and fake-virus simulator worked. Direct popup test returned a usable handle and displayed the qualified Allowed result; Close test window worked.
- Fake-virus demonstration launched with conspicuous fictional labels, inspect buttons, destruction and exit controls.
- Live simulator canonical and OG image URLs match the deployed host/subdirectory.
- Inspected console logs contained browser-extension metadata errors only; no site-origin JavaScript error was observed in these checks.
- Desktop screenshot showed readable targets and weapon controls. No claim is made about real mobile touch, audible output, haptics, Lighthouse or field Core Web Vitals.
