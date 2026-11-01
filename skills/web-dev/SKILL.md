---
name: web-dev
description: General web development work in any frontend or full-stack web codebase. Use when building or changing UI, components, pages, routes, styles, forms, data fetching, or client state, and when reviewing web code for accessibility, performance, and responsive behaviour. Covers React, Next.js, Vue, Svelte, Angular, and plain HTML/CSS/JS projects.
---

# Web Development

Use this skill for everyday web work: adding a component, wiring a page, fixing a layout, hooking up an API call, or cleaning up CSS. It is framework agnostic. The point is to land changes that look like the rest of the codebase and hold up in a real browser, not just in a diff.

## Step 0: Read the project before writing anything

Never guess the stack. Spend a minute on these:

```bash
cat package.json
ls -a
```

Work out, and keep in mind for the whole task:

- **Framework and version.** React vs Next.js App Router vs Pages Router vs Vue vs Svelte vs Angular. Routing and data fetching differ sharply between them.
- **Language.** TypeScript or JavaScript. If TypeScript, match the strictness already in `tsconfig.json` and do not add `any` to get past a type error.
- **Styling system.** Tailwind, CSS Modules, styled-components, Sass, vanilla CSS, or a design system package. Use the one already there. Do not introduce a second styling approach for one component.
- **Component library.** shadcn/ui, MUI, Chakra, Radix, or an in-house package. Reach for an existing component before building a new one.
- **Package manager.** Use the one matching the lockfile (`pnpm-lock.yaml`, `yarn.lock`, `package-lock.json`, `bun.lockb`). Running the wrong one rewrites the lockfile and pollutes the diff.
- **Scripts.** Note the real names for dev, build, lint, typecheck, and test. They are not always `npm run lint`.

Then read two or three files near the one you are changing. Copy their import order, file naming, export style, prop typing, and comment density. Local convention beats any general best practice.

## Step 1: Find what already exists

Most web tasks are half done already somewhere in the repo. Before creating a file, search for:

- A component that does nearly the same thing (a `Button`, `Modal`, `DataTable`, `EmptyState`)
- An existing hook for the same data or the same bit of state
- Design tokens: color, spacing, radius, and font scales in a Tailwind config, a theme file, or CSS custom properties
- A utility for the thing you are about to hand-roll (`cn`, `formatDate`, a fetch wrapper)

Hardcoding `#6E56CF` when the project has `--color-primary`, or writing a fourth bespoke dropdown, is the most common way web changes go wrong.

## Step 2: Build it

### Components

- One clear job per component. Split when a component juggles both data fetching and complex presentation.
- Keep props narrow and typed. Prefer a few explicit props over one wide `options` object.
- Derive state instead of storing it. If a value can be computed from props or other state, compute it.
- Put state as low in the tree as it can live. Lift it only when a sibling genuinely needs it.
- Server components by default in frameworks that have them. Add `"use client"` only for the subtree that needs interactivity, events, or browser APIs.

### Styling and layout

- Mobile first. Write the small-screen layout, then add breakpoints upward.
- Flexbox and grid for layout. Absolute positioning only when the layout genuinely needs it.
- No fixed pixel heights on text containers. Text wraps differently across locales and font sizes.
- Respect dark mode if the project has it. Check every new surface in both themes, including borders and shadows, which commonly disappear in one theme.
- Keep interactive targets at least 44 by 44 pixels on touch.
- Honour `prefers-reduced-motion` for anything that moves.

### Data fetching and state

- Use the project's existing data layer: React Query, SWR, RTK Query, Apollo, a server action, or a plain fetch wrapper. Do not add a new data library for one call.
- Handle all four states every time: loading, empty, error, and success. A screen that only handles success is unfinished.
- Cancel or ignore stale requests when inputs change, so a slow earlier response cannot overwrite a newer one.
- Keep server data out of global client state unless something actually needs it there.
- Never put secrets in client code. Anything in a `NEXT_PUBLIC_`, `VITE_`, or equivalent variable is public.

### Forms

- Use the project's form library if there is one. Otherwise keep inputs controlled and validate on submit plus on blur, not on every keystroke.
- Label every input. A placeholder is not a label.
- Show errors next to the field they belong to, and tie them to the input with `aria-describedby`.
- Disable the submit button while a submission is in flight, and keep the typed values if it fails.

### Accessibility

This is not a polish pass. Build it in as you go:

- Semantic elements first. A `button` for actions, an `a` for navigation, real headings in order.
- Everything clickable must be reachable and operable by keyboard, with a visible focus style.
- `alt` text on meaningful images, `alt=""` on decorative ones.
- ARIA only when no semantic element fits, and never a role that fights the element.
- Check colour contrast on new text and new UI borders.

See `references/review-checklist.md` for the full pass to run before you call the work done.

## Step 3: Verify in a browser, not just in your head

A web change is not done because it compiles. Run the project's own checks, then look at it:

```bash
npm run typecheck && npm run lint
```

Then start the dev server and open the page. Use the browser tools available in this session to:

- Load the route you changed and read the page, not just screenshot it
- Check the console for errors and warnings, including hydration mismatches and React key warnings
- Check the network tab for duplicate or waterfalled requests
- Resize to a narrow viewport and confirm nothing overflows horizontally
- Walk the new UI with the keyboard alone

Fix what you find before reporting. If something genuinely cannot be verified in this environment, say which part and why.

## Common mistakes to avoid

- Adding a dependency when the project already has something that does the job
- A `useEffect` that only syncs state which could have been derived
- Array index as a React `key` on a list that reorders or filters
- Fetching in a child when the parent already has the data
- `div` with an `onClick` in place of a `button`
- A new colour, spacing value, or font size that bypasses the design tokens
- Tailwind class strings built by concatenation that the compiler cannot see, so the class never ships
- Leaving `console.log` or commented-out code in the diff
- Reformatting untouched lines, which buries the real change

## Reporting back

Say what changed, which files, and what you actually verified: the commands you ran and what you checked in the browser. Call out anything left unverified. Plain sentences, no em dashes.
