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
- Embedded Google font declarations for `Space Grotesk`, `Noto Sans`, `Geist Mono`, and local `Good Brush`

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

## Example prompts

- "Create a 12-slide HTML presentation about secure React authentication with a portfolio-style dark theme."
- "Generate a slide deck for a technical talk on web performance optimization using Brion Mario's portfolio visual system."
- "Turn this outline into a single-file HTML presentation with scroll-snap slides and bold headings."

## Notes

- This skill should be used together with the `frontend-design` skill for refined color, typography, and layout decisions.
- Prefer custom slide structures over generic slide templates.
- Use the portfolio's dark background, vivid accent, and strong typography as the foundation for every deck.
