# Project overview

Orbital is a standalone space-exploration quiz. All application markup, CSS,
inline SVG artwork, question data, and JavaScript live in `index.html`.

## Running and dependencies

- Open `index.html` directly in a browser using a `file://` URL.
- No server, package manager, build step, framework, or external dependencies
  are required. Keep the application self-contained and usable offline.
- Do not introduce external fonts, CDN assets, network requests, or additional
  application files unless explicitly requested.
- This workspace currently has no Git repository or automated test suite.

## Implementation conventions

- Use vanilla HTML, CSS, and JavaScript with the existing two-space indentation.
- Keep CSS in the inline `<style>` block and JavaScript in the inline `<script>`
  block. The script uses strict mode.
- Reuse the `$` helper for element lookup and the existing render, selection,
  results, and replay functions.
- Create dynamic content with DOM methods and `textContent`, rather than
  interpolating content into `innerHTML`.
- Keep question records consistent: `category`, `question`, four `options`,
  zero-based `correct` index, and explanatory `fact`.

## Behavior to preserve

- The quiz has 10 questions and awards one point per correct answer.
- Each question can be answered once. Disable all answers after selection and
  prevent repeated input from changing the score.
- Progress represents questions answered, not questions merely displayed.
- Correct answers receive green feedback and a pop animation. Incorrect
  answers receive red shake feedback and reveal the correct option.
- Number keys 1-4 select answers. Ignore modified and repeated key events, and
  disable shortcuts after answering and while results are visible.
- Results show score, correct and missed counts, accuracy, and an emoji.
- Scores of 8 or higher receive mission honors and confetti; a perfect 10 has
  distinct messaging. Lower scores must not receive the high-score treatment.
- Replay resets score, progress, feedback, status, and celebration state.

## Design and accessibility

- Preserve the centered, responsive, narrow column with a 500px maximum width,
  sans-serif body text around 14-16px, and mission-control styling.
- Reuse semantic CSS custom properties from `:root`; maintain both light and
  dark palettes selected by `prefers-color-scheme`.
- Preserve the star-field background without obscuring content or controls.
- Respect `prefers-reduced-motion`. Decorative effects should remain static
  with that preference enabled; avoid adding unconditional animated effects.
- Use native buttons, visible keyboard focus, descriptive labels, and the
  existing polite, atomic feedback live region.
- Do not rely on color alone to communicate correctness. Retain text and marks.
- Preserve focus transitions to Next after an answer, the question after
  advancing or replaying, and the results heading on completion.
- Keep decoration hidden from assistive technology where appropriate and
  non-interactive with `pointer-events: none`.

## Validation

- For behavior changes, smoke-test the actual page in a browser: initial state,
  correct and incorrect answers, score updates, answer locking, all 10 questions,
  progress, results totals, and replay.
- Check high-score boundaries at 7, 8, and 10.
- For visual changes, check narrow viewports, both color schemes, reduced motion,
  readable contrast, visible focus, and absence of horizontal overflow.
- Test native Tab and Enter/Space interaction when the browser tooling supports
  it. Dispatched DOM keyboard events can test shortcut handlers but do not prove
  native keyboard traversal or activation; report that limitation honestly.
- Refresh the integrated browser after changes when it is open. Do not add
  dependencies solely for validation.
