# Slide Templates

Use these slide patterns as starting points. Keep every slide full-screen, visually balanced, and aligned with the portfolio-inspired dark theme.

## 1. Title slide

Ideal for the beginning of the deck.

```html
<section>
  <div class="slide hero">
    <div class="eyebrow">Talk</div>
    <h1 class="slide-title">Presentation Title</h1>
    <p class="slide-subtitle">One sentence describing what the audience will learn and why it matters.</p>
    <div class="label-row">
      <span class="label-pill">Topic</span>
      <span class="label-pill">Role</span>
      <span class="label-pill">Event</span>
    </div>
  </div>
</section>
```

## 2. Statement / quote slide

Use when you want a bold claim, thesis, or memorable quote.

```html
<section>
  <div class="slide">
    <div class="quote">
      “A strong presentation feels like a branded web experience, not a generic template.”
      <cite>— Speaker name</cite>
    </div>
  </div>
</section>
```

## 3. Content grid / cards

Ideal for features, benefits, or multiple points.

```html
<section>
  <div class="slide grid columns">
    <div class="card">
      <h3>Point One</h3>
      <p>A short phrase with explanation and impact.</p>
    </div>
    <div class="card">
      <h3>Point Two</h3>
      <p>Keep copy clear and concise. Use 2–3 lines.</p>
    </div>
  </div>
</section>
```

## 4. Comparison slide

Use a two-column layout for before/after, old/new, pros/cons.

```html
<section>
  <div class="slide comparison">
    <div>
      <p class="big-label">Before</p>
      <h2>Old approach</h2>
      <p>Describe the challenge or limitation of the current state.</p>
    </div>
    <div>
      <p class="big-label">After</p>
      <h2>New approach</h2>
      <p>Explain the improved result and why it matters.</p>
    </div>
  </div>
</section>
```

## 5. Stats / results slide

Use big numbers for impact.

```html
<section>
  <div class="slide stat-grid">
    <div class="stat">
      <strong>4.5×</strong>
      Faster load times
    </div>
    <div class="stat">
      <strong>98%</strong>
      User satisfaction
    </div>
    <div class="stat">
      <strong>1 file</strong>
      Single HTML export
    </div>
  </div>
</section>
```

## 6. Screenshot / visuals slide

Give screenshots their own dedicated slide.

```html
<section>
  <div class="slide">
    <div class="big-label">Visual preview</div>
    <div class="screenshot"></div>
    <p class="slide-subtitle">Use a clean frame or screenshot card to show product UI, architecture diagrams, or screenshots.</p>
  </div>
</section>
```

## 7. Diagram / process slide

Use clear labels, lines, or structure elements.

```html
<section>
  <div class="slide">
    <div class="big-label">Process</div>
    <h2>How the system works</h2>
    <div class="card">
      <p>Step 1 — Outline the first key action.</p>
      <p>Step 2 — Explain the second stage succinctly.</p>
      <p>Step 3 — Share the final outcome.</p>
    </div>
  </div>
</section>
```

## 8. Closing / contact slide

Finish with a strong call to action.

```html
<section>
  <div class="slide">
    <div class="slide-num">Last slide</div>
    <div class="big-label">Thank you</div>
    <h2 class="slide-title">Let’s build something great together.</h2>
    <div class="footer"><strong>Contact</strong> hello@brionmario.com</div>
  </div>
</section>
```

## Layout hints

- Use `section` for each slide and keep content inside a centered `.slide` container.
- Prefer `grid` layouts for balanced spacing.
- Keep copy short and avoid dense paragraphs.
- Use `.big-label`, `.slide-num`, and `.eyebrow` sparingly to create hierarchy.
- Use the accent palette only for emphasis; keep the main background and surfaces dark.
