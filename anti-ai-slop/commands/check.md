---
description: Review code or design for AI-slop patterns and fix them
argument-hint: [files or nothing for recent changes]
---

Check the given files (or, if none were given, the recent uncommitted changes) against the
`anti-ai-slop` skill rules: banned vocabulary; emoji in UI copy, comments, logs or commits;
purple/neon gradients and gradient text; Inter/Roboto as font choice; glassmorphism and blur spam;
uniform card grids; over-commenting and obvious narration; defensive boilerplate and swallowed
errors; unrequested features or abstractions; style mismatch with the surrounding codebase;
bloated README/commit scaffolding.

For each finding report: file, line, what the slop is, and the concrete human replacement.
Then apply the fixes — unless the pattern was explicitly requested by the user.
