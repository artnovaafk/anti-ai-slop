---
description: Review code, design or text for AI-slop patterns and fix them
argument-hint: [files or nothing for recent changes]
---

Check the given files (or, if none were given, the recent uncommitted changes) against the
`anti-ai-slop` skill rules: banned vocabulary; emoji in UI copy, comments, logs or commits;
purple/neon gradients, gradient text, gradient orbs and Tailwind blue-500/indigo-600 defaults;
Inter/Roboto as font choice or untouched shadcn styling; glassmorphism and blur spam; uniform
card grids and hover:scale everywhere; fake testimonials; template hero+pricing pages; generic
marketing copy; over-commenting and obvious narration; defensive boilerplate, broad except on
one-offs and swallowed errors; generic verb-sludge names (handleClick, processData), junk-drawer
utils modules, dead imports, tautological tests; unrequested features or abstractions; style
mismatch with the surrounding codebase; bloated README/commit scaffolding; sycophancy openers,
restated requests, performative endings, forced rule-of-three and bullet-spam in any text.

For each finding report: file, line, what the slop is, and the concrete human replacement.
Then apply the fixes — unless the pattern was explicitly requested by the user.
