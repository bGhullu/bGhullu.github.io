# Public Engineering Portfolio

A standalone, static portfolio site presenting two engineering efforts from the same
problem space:

1. **Legacy MEV Arbitrage System** — an established, event-driven multi-DEX arbitrage
   system in Rust with a Solidity flashloan executor.
2. **System Re-Architecture** — a milestone-controlled clean-room rebuild of that system,
   explicitly labelled **Work in Progress**.

It is deliberately **static**. There is no build step, no bundler, no package manager, no
framework, and no runtime service. It can be copied into an empty GitHub repository and
served directly by GitHub Pages.

---

## Structure

```text
public-portfolio/
├── .nojekyll                               # disables Jekyll — files served byte-exact
├── index.html                              # Home: projects, evolution, evidence, practice
├── styles.css                              # Single stylesheet, no build step
├── assets/
│   ├── favicon.svg
│   ├── legacy-flow.svg                      # Level 1 diagram — legacy system
│   └── rearchitecture-flow.svg              # Level 1 diagram — re-architecture
├── projects/
│   ├── legacy-arbitrage-system.html        # Project 01 case study
│   └── re-architecture.html                # Project 02 case study (WIP)
└── README.md
```

All links are relative. The site works from `file://`, from a subpath, and from a
repository root — no configuration required.

---

## Evidence-level labels

Every substantive claim on the site carries one of these labels, used consistently:

| Label | Meaning |
|---|---|
| `IMPLEMENTED` | Built and present in the codebase |
| `VERIFIED` | Independently checked — gate, re-execution, or re-derivation |
| `DOCUMENTED` | Recorded in a specification or design artifact; not necessarily built |
| `IN PROGRESS` | Actively being worked; not finished |
| `PLANNED` | Specified but not implemented |
| `NOT ESTABLISHED` | The record does not support this claim — stated as a gap |

Rules observed when writing this site:

- `PLANNED` is never presented as `IMPLEMENTED`.
- `NON-LIVE` is never presented as `PRODUCTION`.
- `TESTED` is never presented as `DEPLOYED`.
- Every number is quoted from a written artifact and carries its provenance.
- Where an artifact itself records a limitation (a review not re-run, a caveat about
  review independence), the limitation is repeated rather than dropped.

---

## What is deliberately excluded

This portfolio is a demonstration of engineering judgement, not a reproducibility guide.

Not published, and not to be added:

- Complete algorithms, search strategies, or opportunity-selection logic
- Complete execution or transaction-construction logic
- Proprietary heuristics, ranking formulas, thresholds, or tuning values
- Contract addresses, deployment details, or full contract interaction flows
- Internal infrastructure topology, hostnames, network layout, or endpoints
- Configuration values, environment files, keys, or credentials of any kind
- Internal report filenames, private paths, or repository metadata
- Any material sufficient to reproduce or clone the system

Sanitized explanations and diagrams are used instead of source excerpts throughout.

---

## Running locally

Open `index.html` in a browser, or serve the folder:

```bash
cd public-portfolio
python3 -m http.server 8000
# then open http://localhost:8000
```

---

## Deploying to GitHub Pages

> ### ⚠️ Read this first — the publishing source is the whole branch root
>
> GitHub Pages publishes the **entire** source folder. Its only options are a branch's `/`
> root or a `/docs` folder — **there is no "publish a subfolder" mode**. Anything else living
> on that branch becomes publicly reachable by direct URL.
>
> The destination repository must contain **only these files**. Verify before pushing:
>
> ```bash
> ls -A
> # expect exactly: .nojekyll  README.md  assets  index.html  projects  styles.css
> ```
>
> Never enable Pages on a branch that also carries application source, reports, config or
> history you intend to keep private.
>
> Also note: GitHub states that *"Pages sites are publicly available on the internet, even if
> the repository for the site is private."* On the **Free** plan Pages requires a **public**
> repository; private-repo Pages requires Pro / Team / Enterprise Cloud.

1. Create a new **public** repository (separate from any private source repository):

   ```bash
   mkdir portfolio-site && cd portfolio-site
   git init -b main
   ```

2. Copy the **contents** of `public-portfolio/` into it (not the folder itself):

   ```bash
   cp -R /path/to/mev/public-portfolio/. .
   ls -A     # must list the six entries shown above
   ```

   `.nojekyll` is a hidden file — confirm it copied. It tells GitHub not to run Jekyll, so
   your HTML, CSS and SVG are served byte-exact instead of being rewritten
   (`README.md` → `README.html`).

3. Commit and push:

   ```bash
   git add -A
   git commit -m "Publish engineering portfolio"
   git remote add origin <YOUR_PUBLIC_REPO_URL>
   git push -u origin main
   ```

4. In the GitHub repository: **Settings → Pages → Source → Deploy from a branch**,
   branch `main`, folder `/ (root)`. Save.

5. The site appears at `https://<username>.github.io/<repo>/` within a minute or two.

Because everything is relative, no `baseurl` or path configuration is needed.

> **Before publishing:** re-run the leakage check described in the build report. The
> folder must contain no secrets, no internal paths, no private URLs, and no report
> filenames.

---

## Content sources

The site's content is derived from the project's own engineering record — milestone
implementation reports, independent adversarial gate verdicts, test baselines, closure
adjudications, and ratified architecture specifications. Source code was consulted only
selectively, to confirm that specific described components exist.

Nothing on this site is inferred from memory, and no metric is extrapolated.

---

## Disclaimer

Research and educational software. Not financial advice. Not a live trading service.
No claim of profitability, production deployment, or completed status is made.
