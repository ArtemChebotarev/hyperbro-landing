# Hyperbro landing — project context

Documentation and comments are written in English.

Static site for the Hyperbro iOS app at https://hyperbro.app: `index.html` (the landing, inline CSS/JS), `support.html`, `privacy-policy.html` (shared styles in `assets/legal.css`), `images/`, `og-image.png` (1200×630 link preview). GitHub Pages serves `main` from the repo root; the domain is set in `CNAME` (DNS on Cloudflare). There is no build step and no CI: whatever is merged into `main` is live about a minute later.

Project folder on disk: `~/hyperbro-landing`. To commit, push and open a PR, use the `commit-and-push` skill.

# Git workflow

`main` is protected on GitHub (ruleset `main-protection`): every change reaches it through a pull request; direct pushes, force-pushes and deleting `main` are rejected. Never commit on `main` and never try to push to it.

- Before starting any task that touches files, run `git fetch origin` and fast-forward local `main` to `origin/main`. Then branch off it: `feat/<short-name>`, `fix/<short-name>`, `copy/<short-name>` (text-only changes), `chore/<short-name>`.
- One task, one branch, one PR into `main`. Keep unrelated changes out of it.
- Merging a PR publishes the site, so **Artem merges** — never merge a PR yourself, never enable auto-merge, unless Artem explicitly asks for that PR in the current conversation.
- Pushing a task branch and opening or updating its PR is fine once the work is checked; it changes nothing on the live site.

# Before a PR

- Preview locally: `.claude/launch.json` has a `landing` config (`python3 -m http.server 8787`). Open the changed pages at desktop and phone widths and check the console for errors. Visual changes are shown to Artem before the PR.
- The Python server does not resolve extensionless URLs, so internal links use `.html` (`support.html`, not `/support`); GitHub Pages serves both.
- When a stylesheet changes, bump its `?v=` query in every page that links it, otherwise browsers keep the cached copy.
- Images: WebP for page images; `og-image.png` stays 1200×630 PNG. Messengers cache link previews per URL — a new preview needs a new image URL (e.g. `og-image.png?v=2` in `og:image` and `twitter:image`).
- The App Store badge (`assets/brand/app-store-badge.svg`) is Apple's official artwork: never edit it, keep it at least 40 px tall with clear space of a quarter of its height.
- App Store links carry campaign tokens (`pt`, `ct`) built in the page script — keep the `js-appstore` class and `data-cta` on new App Store buttons instead of hard-coding the URL.
- `privacy-policy.html` has maintenance notes at the top: anything the site or the app starts collecting means updating that page first.
