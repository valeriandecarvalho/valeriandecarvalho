# Design · Profile presentation

## Visual structure

1. Language disclosures: **EN open by default**; FR can be expanded to the same complete layout. GitHub HTML rendering may not behave as an exclusive tab switch; the content remains accessible either way.
2. Banner: same composition in English and French; no disposable labels or technical buzzwords in the image.
3. Introduction: short, timeless, centered.
4. Portfolio: the main destination; GitHub and LinkedIn grouped under Socials / Réseaux.
5. Toolbox: two continuous rows of **20 genuine technology logos each**, without categories or individual captions. First row moves left, second moves right.
6. Contributions: auto-updated, theme-aware snake.
7. Contact: public professional email and LinkedIn; do not publish a non-functional email address.

## Color palette

| Use | Light | Dark |
| --- | --- | --- |
| Banner background | Sage/cream artwork | Forest/charcoal artwork |
| Toolbox background | `#F3F8EF` | `#10271E` |
| Empty contribution tile | `#E8F1E5` | `#1B2521` |
| Contribution level 1 | `#D2E6C6` | `#2F4A3C` |
| Contribution level 2 | `#A9D28E` | `#4F7A60` |
| Contribution level 3 | `#6FA85F` | `#78B178` |
| Contribution level 4 / snake | `#1E5A47` | `#B9D99A` |

## Theme switching

`README.md` uses `<picture>` with `media="(prefers-color-scheme: dark)"`; each visitor sees the version corresponding to **their GitHub theme preference**, not the author's preference. The moving toolbox also supplies static first-frame PNGs for browsers that support `prefers-reduced-motion: reduce`.

## Toolbox assets

The real GIFs must be built from the **official SVG technology marks** using `BUILD/build_official_logos.py` in the installation package. Do not ship example/demo GIFs in the published README. The completed build writes a verification manifest and static fallbacks.

The generator depends on Devicon and Simple Icons **at build time**, not on external image URLs when someone visits the profile. Review each icon's trademark/brand requirements if reusing the design elsewhere.

## Language and contact maintenance

- Keep all visual sections in both languages; translate only the text.
- The contact address is a proposed domain email. Configure receiving (and ideally sending) before publication.
- Keep `README.md` short. Technical details belong under `docs/`, not in the public profile introduction.
