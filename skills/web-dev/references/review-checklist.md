# Pre-handoff checklist

Run this before reporting a web change as done. Skip nothing silently: if an item does not apply, it does not apply, but if you could not check it, say so.

## Build and types

- [ ] Typecheck passes with no new errors
- [ ] Lint passes with no new warnings
- [ ] Build succeeds, if the change touches routing, config, or imports
- [ ] No new `any`, `@ts-ignore`, or disabled lint rules added to get past an error
- [ ] Lockfile unchanged unless a dependency was genuinely added

## Browser

- [ ] The changed route loads
- [ ] Console is clean: no errors, no hydration mismatch, no missing-key warnings
- [ ] Network tab shows no duplicate or needlessly sequential requests
- [ ] Loading, empty, error, and success states all render
- [ ] Nothing overflows horizontally at 375 pixels wide
- [ ] Layout holds at a wide viewport too, with no stretched line lengths
- [ ] Both light and dark themes look right, including borders and shadows

## Keyboard and screen reader

- [ ] Every interactive element is reachable by Tab, in a sensible order
- [ ] Focus is visible on each one
- [ ] Enter and Space activate buttons, Escape closes overlays
- [ ] Focus is trapped inside a modal while open and returns to the trigger on close
- [ ] Each input has a real label
- [ ] Error messages are tied to their field
- [ ] Images have `alt` text, or `alt=""` when decorative
- [ ] Headings are in order, with no level skipped

## Content and copy

- [ ] Long strings and long words do not break the layout
- [ ] Empty states say something useful, not just "No data"
- [ ] Error messages say what happened and what to do next
- [ ] Dates, numbers, and currency go through the project's formatting helpers
- [ ] No lorem ipsum or placeholder text left behind

## Code quality

- [ ] Follows the surrounding file's conventions for naming, imports, and structure
- [ ] No duplicated component or hook that already existed
- [ ] Colours, spacing, and type come from design tokens
- [ ] No debug logging, dead code, or commented-out blocks
- [ ] Diff touches only what the task needed, with no drive-by reformatting
