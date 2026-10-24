# go

Personal short-link redirector for Rick Howard's GitHub-hosted content — primarily links into the private `raceBannon99/nexus-artifacts` repo (Alexandria's Library), where a long `github.com/login?return_to=...` URL would otherwise wrap in a terminal and break.

**How it works**: every short link is `https://racebannon99.github.io/go/<code>`. There's no real path at `<code>`, so GitHub Pages serves `404.html`, which fetches `redirects.json`, looks up `<code>`, and client-side-redirects to the real (long) target URL.

**Known tradeoff, accepted deliberately**: `redirects.json` is a public file. Anyone who finds this repo can see every short code's *target URL* — which, for a private-repo link, reveals that artifact's title/filename (not its content; the content itself still sits behind GitHub's own login on the private repo). This repo exists because that tradeoff was judged acceptable in exchange for links that don't break in a terminal. See `raceBannon99/nexus-artifacts`'s own README for why the underlying repo is private in the first place.

**Maintenance**: codes are assigned once and never reused or repointed — `redirects.json` only ever grows. Managed by the `nexus-artifact-list` skill in `raceBannon99/The-Nexus`'s companion vault project.

**Known bug, fixed 2026-10-24**: `404.html`'s fetch of `redirects.json` originally had no cache-busting. A visitor who'd already loaded an older short link in the same browser session (caching `redirects.json` from before a new code was added) would get "Unknown short link: `<code>`" on a brand-new code, even though the file on GitHub was already current — the browser (and/or GitHub Pages' own CDN) was serving a stale cached copy instead of re-fetching. Fixed by appending a cache-busting `?v=<timestamp>` query string and setting `{ cache: 'no-store' }` on the fetch, so every visit always pulls the live file regardless of what was cached from an earlier visit.
