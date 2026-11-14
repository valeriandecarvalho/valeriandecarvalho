# Profile system · Overview

**Repository:** [`valeriandecarvalho/valeriandecarvalho`](https://github.com/valeriandecarvalho/valeriandecarvalho)  
**Purpose:** Serve a bilingual GitHub profile and display a regularly generated contribution snake. This is **not** the source code for the personal portfolio website.

## What visitors see

- A light/dark adaptive banner with a single name.
- An English and French introduction (native HTML `<details>` disclosures; English open by default).
- A prominent link to the [portfolio](https://valeriandecarvalho.com), then GitHub and LinkedIn links.
- A two-row scrolling toolbox with **40 logos** (20 to the left, 20 to the right). The GIFs are locally stored; no runtime icon CDN is necessary.
- An animated contribution snake, in a light/dark variant.
- An email and LinkedIn contact section. The `contact@valeriandecarvalho.com` mailbox **must exist before the email button is usable**.

## Repository structure

```text
main/
├── README.md                    Public profile content (EN + FR)
├── assets/
│   ├── brand/                  Light/dark banners
│   ├── links/                  Portfolio and contact SVG buttons
│   └── toolbox/                Two animated GIFs, static fallbacks, optional source icons
├── .github/workflows/snake.yml  Daily snake generation
└── docs/
    ├── overview.md             This document
    ├── architecture.md         GitHub + GitLab interactions
    ├── design.md               Assets, themes and language parity
    └── maintenance.md          Updates, checks and recovery

output/
├── github-snake.svg            Generated light snake
└── github-snake-dark.svg       Generated dark snake
```

The GitLab project is a **separate repository**: [`valeriandecarvalho1/github-snake-automation`](https://gitlab.com/valeriandecarvalho1/github-snake-automation). It checks that the generated snake is recent and regenerates it when necessary.

## Operating principles

1. **GitHub `main` is manually maintained.** Changes are reviewed and published intentionally; no scheduled job writes to it.
2. **GitHub `output` is generated.** Its two SVG files are maintained automatically; each snapshot has **one parentless commit**.
3. **GitLab `main` is manually maintained.** The fallback job reads it, never changes it.
4. By project convention, both source branches `main` are also kept at **one root commit**. This is *not* normal Git practice; changing `main` requires deliberate history rewriting, backups and `--force-with-lease`.
5. Light/dark palette changes must be synchronized in **both** the GitHub workflow and the GitLab generation script.

See [Architecture](architecture.md), [Design](design.md) and [Maintenance](maintenance.md).
