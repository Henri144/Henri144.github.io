<!-- Project-specific Copilot instructions for Trainsounds -->
# Copilot instructions — GOPO Trains Soundboard

Purpose
- Help AI coding agents make small, safe edits to the single-page soundboard and its assets.

Project overview (big picture)
- A single static HTML page: [Trains.html](Trains.html). The UI, styles, and logic live inline.
- Audio assets live in the `sounds/` directory. Sounds are referenced by URL from the `pads` array inside `Trains.html`.
- There is no build system, bundler, or tests — changes should be minimal and keep everything runnable by opening `Trains.html` in a browser or serving with a simple HTTP server.

Key files and locations
- Main app: [Trains.html](Trains.html)
- Assets: `sounds/` (place .mp3/.wav here and reference them from `Trains.html`)

How the code is structured (what to edit)
- Pads data: edit the `pads` array in `Trains.html` to add/remove sounds. Example entry:

  { name: "Choo Choo!", url: "sounds/ChooChoo.wav" }

- Playback: `playSound(pad)` creates a new `Audio(pad.url)` and uses a Set `activeAudios` to track active audio objects. To stop all sounds, call the existing `stopAll()` function.
- UI: the visual styles are inline in the `<style>` block at the top of `Trains.html`. Follow the existing CSS variables (`--wood-dark`, `--brass`, etc.) when adding UI elements.

Developer workflows (quick commands)
- Preview locally (recommended when adding/renaming audio files):

  python -m http.server 8000

  Then open http://localhost:8000/Trains.html in a browser.

- No npm/node tooling present — avoid introducing tooling unless requested by repo owner.

Project-specific patterns & constraints
- Single-file app: prefer small, self-contained edits inside `Trains.html` rather than extracting pieces unless asked.
- Audio must be served over HTTP/HTTPS to play reliably in modern browsers; opening the file via the `file://` protocol can cause CORS or autoplay issues.
- Browser autoplay restrictions: playback must be triggered by a user gesture. The current code relies on click events (keep that pattern).
- Asset paths are relative and case-sensitive on some filesystems; place new audio files in `sounds/` and reference them with forward slashes.

Safety and style guidance for AI edits
- Preserve the single-file approach. If a change requires creating new files, ask before adding build or runtime dependencies.
- Keep UI style consistent: reuse CSS variables and existing class names like `.pad` and `.play`.
- For changes to playback logic, prefer using the existing `activeAudios` Set and the `stopAll()` helper rather than rewriting playback lifecycle.

Examples of acceptable changes
- Add a new pad entry to `pads` to expose another sound.
- Improve the toast messages or add a short visual indicator next to pads (modify inline HTML/CSS/JS in `Trains.html`).
- Implement a small accessibility improvement (e.g., add `aria-label` to buttons) directly in `Trains.html`.

When to ask the human owner
- Before introducing any new build tools, package managers, or test frameworks.
- When a change touches more than ~40 lines of `Trains.html` or creates new top-level files.

If something seems missing
- If you need a project README or test harness, ask — this repo currently contains only `Trains.html` and `sounds/`.

Done: this file is a baseline. Reply with areas to expand (examples, tests, or migration to modular structure).
