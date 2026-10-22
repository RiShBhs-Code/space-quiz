# Copilot instructions

## Project overview

This repository is a dependency-free, single-page browser quiz. The complete application lives in `index.html`: markup, component styling, quiz data, state management, rendering, interaction handlers, accessibility behavior, and animations are all kept together so the file can be opened directly with no server.

The quiz is driven by the `questions` array. `current` tracks the active question and `score` tracks correct answers. `renderQuestion()` rebuilds the answer buttons and progress UI for the current item; `chooseAnswer()` disables choices, applies correct/wrong feedback, and advances after a short delay; `showResults()` swaps the quiz card for the results card and starts the score animation. Keep changes aligned with this data-to-DOM flow rather than adding duplicated question-specific markup.

## Build, test, and lint

There is no `package.json`, build system, test runner, or linter. Do not add dependency or tooling requirements for routine changes. Open `index.html` directly in a browser for a manual smoke test.

For a focused manual check of a quiz change:

1. Open `index.html`.
2. Activate each answer using keyboard focus and Enter/Space.
3. Confirm progress, score, feedback, and the results/restart flow.
4. Check both light and dark color schemes and reduced-motion behavior when those preferences are available.

## Conventions

- Keep the app self-contained in `index.html`; use no external scripts, stylesheets, fonts, servers, or dependencies unless the project requirements explicitly change.
- Put reusable visual values in the CSS custom properties under `:root`, with corresponding overrides inside `@media (prefers-color-scheme: dark)`.
- Preserve the existing semantic controls and focus behavior: answer choices and restart are native `<button>` elements, question/results headings receive focus when views change, and live regions announce score and feedback changes.
- Preserve motion accessibility. Any new animation should have an appropriate `prefers-reduced-motion: reduce` behavior.
- Keep question content in the `questions` data array. Each item uses `{ question, answers, correct }`, where `correct` is the zero-based answer index.
- JavaScript is wrapped in an IIFE with `"use strict"`; retain that isolation style and use the existing cached DOM references and small single-purpose functions.
- Use the existing CSS class states (`correct`, `wrong`, `shake`, and `hidden`) for interaction and view transitions instead of inline style logic where possible.
- Maintain the current visual language: rounded translucent cards, CSS variables for theme colors, responsive layout, and space-themed emoji/text.
