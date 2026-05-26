# My Personal Dashboard

A static personal dashboard for Abhinav with a Miles Morales inspired bento interface. The page combines focus tools, local notes, audio controls, an AI news stream, and a terminal-style command panel in a single `index.html` file.

## What It Includes

- Responsive frosted-glass bento layout
- Dark default theme with a light-theme toggle
- Live local clock and greeting
- Cursor particle effect with reduced-motion support
- Pomodoro focus and break timer
- Audio player with playlist, volume control, and canvas visualizer
- AI news stream with offline fallback cards
- Local browser notes using `localStorage`
- Terminal-style command console

## Repository Structure

- `index.html` - Main static app: markup, Tailwind CDN config, CSS, and JavaScript.
- `DESIGN.md` - Visual design system and theme guidance.
- `agent.md` - Operating notes for AI coding agents.
- `.nojekyll` - Disables Jekyll processing for GitHub Pages.
- `ribbed_glass.jpg` - Background texture.
- `spiderman.png` - Backdrop artwork.

## Run Locally

No install step is required.

Open `index.html` directly in a browser, or serve the folder with a static server:

```bash
python -m http.server 8000
```

Then open `http://localhost:8000`.

## External Services

The dashboard is static, but some browser-side features use external network resources:

- Tailwind CSS CDN
- Google Fonts
- SoundHelix demo audio files
- TechCrunch AI RSS feed through `rss2json`

The page includes fallback behavior so the core dashboard still works if external services fail.

## Notes And Privacy

Notes are saved only in the browser with `localStorage`. The app does not store secrets in the repo and does not ship a browser-side Notion token flow.

## Design Direction

The visual system is defined in `DESIGN.md`: crimson accent `#ff1722`, deep dark canvas, frosted glass cards, squircle corners, tactical typography, and an 8px spacing rhythm.
