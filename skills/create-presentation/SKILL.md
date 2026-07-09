---
name: create-presentation
description: Create polished HTML slide presentations with the look and feel of Brion Mario's portfolio brand. Use when generating a single-file HTML slide deck from a script, outline, or topic brief.
---

Use this skill to generate single-file HTML presentations from scripts, outlines, or topic briefs. The output should feel like a custom, web-native slide deck with Brion Mario's portfolio design language: dark mode, bold typography, purposeful spacing, and subtle glassy gradients.

## What this skill produces

- A single `.html` slide deck with embedded CSS and JS
- Smooth scroll-snap navigation and keyboard controls
- A strong visual hierarchy using portfolio-inspired typography
- Dark theme styling with your portfolio color palette
- Slide-specific layouts for titles, quotes, comparisons, stats, screenshots, and diagrams
- Self-contained font embedding (base64 or local files copied alongside the deck) for `Space Grotesk`, `Noto Sans`, `Fira Code`/`Geist Mono`, and `Good Brush` — no external font CDN calls

## Design principles

- Dark presentation aesthetic with bright, saturated accents
- Bold, expressive headings and clean body copy
- One full-viewport slide per section; no vertical overflow within slides
- Minimal, custom styles instead of generic template look
- Distinctive typography pairing:
  - `Space Grotesk` for headings
  - `Noto Sans` for body text
  - `Geist Mono` for code/labels
  - `Good Brush` for decorative accents and hero titles
- Use portfolio-like color accents: vivid purple, luminous blue, and rich charcoal backgrounds

## Process

1. Read the input thoroughly.
2. Identify the narrative structure, key sections, and slide-worthy moments.
3. Choose slide types from the following patterns:
   - Title / hero slide
   - Statement / quote slide
   - Content grid / feature cards
   - Comparison / before-after slide
   - Stats / result highlights
   - Diagram / flow slide
   - Screenshot showcase
   - Team / contact slide
4. Build slide markup using simple, semantic HTML.
5. Apply the portfolio-inspired theme and animations.
6. Ensure each slide fits in one viewport and navigation dots are generated.
7. Include a small JS section for scroll snapping, active dot highlighting, and arrow-key navigation.

## Presentation rules

- One slide per viewport: every slide must fit in `100vh` × `100vw`.
- No scrolling inside slides. Break content into multiple slides instead.
- Keep text concise and scannable.
- Use strong contrast and intentional accent color sparingly.
- Every deck must include a title slide and a closing/contact slide.

## Portability rules

- The presentation must be fully self-contained and must work offline, with no internet access.
- Never reference files by absolute path or by a path outside the presentation's own folder (e.g. `assets/` paths from this skill, or files elsewhere on disk). If an asset is needed (avatar, logo, font, image), copy it into a folder next to the presentation's `.html` file and reference it with a relative path.
- Never load fonts, icons, or scripts from an external URL (e.g. Google Fonts, CDNs). Embed fonts and small assets as base64 data URIs directly in the HTML/CSS, or copy the font/image files next to the presentation and reference them with relative paths.
- Before finalizing, verify every `src`/`href`/`url()` in the deck is either a relative path to a file shipped alongside it or a data URI — none should point outside the presentation's own directory or to the network.

## Example prompts

- "Create a 12-slide HTML presentation about secure React authentication with a portfolio-style dark theme."
- "Generate a slide deck for a technical talk on web performance optimization using Brion Mario's portfolio visual system."
- "Turn this outline into a single-file HTML presentation with scroll-snap slides and bold headings."

## Notes

- This skill should be used together with the `frontend-design` skill for refined color, typography, and layout decisions.
- Prefer custom slide structures over generic slide templates.
- Use the portfolio's dark background, vivid accent, and strong typography as the foundation for every deck.
- Brion's avatar images are available in `assets/` (`brion-avatar-blue.png`, `brion-avatar-pink.png`, `brion-avatar-yello.png`). Use one when a slide (e.g. title, team, or contact slide) calls for a personal avatar/headshot.
- Brion's profile links (blog, LinkedIn, GitHub, Medium, X, etc.) are listed in `references/links.md` — check them and ask which ones fit the deck's context when building a contact/closing slide, rather than listing all of them by default.
- Font files for main banners are bundled in `assets/fonts/` and listed in `references/fonts.md` (`Space Grotesk` for headings, `Fira Code` for code, `Noto Sans` for body text).
- WSO2 logos are available in `assets/logos/` (`wso2-logo-white.png`, `wso2-logo-black.png`). Use the white version on dark backgrounds and the black version on light backgrounds, e.g. for decks about Brion's work at WSO2.
- Social/platform icons are available in `assets/logos/` for use alongside `references/links.md`: `linkedin.svg`, `github.svg`, `x-twitter.svg`, `medium.jpeg`. Use `brionmario-memoji.png` specifically to represent Brion's portfolio/personal site link.
