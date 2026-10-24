# go

Personal short-link redirector for Rick Howard's GitHub-hosted content — primarily links into the private `raceBannon99/nexus-artifacts` repo (Alexandria's Library), where a long `github.com/login?return_to=...` URL would otherwise wrap in a terminal and break.

**How it works**: every short link is `https://racebannon99.github.io/go/<code>`. There's no real path at `<code>`, so GitHub Pages serves `404.html`, which fetches `redirects.json`, looks up `<code>`, and client-side-redirects to the real (long) target URL.

**Known tradeoff, accepted deliberately**: `redirects.json` is a public file. Anyone who finds this repo can see every short code's *target URL* — which, for a private-repo link, reveals that artifact's title/filename (not its content; the content itself still sits behind GitHub's own login on the private repo). This repo exists because that tradeoff was judged acceptable in exchange for links that don't break in a terminal. See `raceBannon99/nexus-artifacts`'s own README for why the underlying repo is private in the first place.

**Maintenance**: codes are assigned once and never reused or repointed — `redirects.json` only ever grows. Managed by the `nexus-artifact-list` skill in `raceBannon99/The-Nexus`'s companion vault project.
