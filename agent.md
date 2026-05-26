# Agent Guide

This file is for AI coding agents such as Codex, Claude Code, and similar tools working on this repository. It explains what the project is, how it is structured, and how to make changes safely.

## Project Summary

`My-personal-dashboard` is a static personal dashboard for Abhinav with a Miles Morales / Spider-Verse inspired visual system. It is a high-contrast, frosted-glass bento dashboard with focus tools, local notes, audio controls, an AI news stream, and a terminal-style command panel.

The project is intentionally compact. There is no build system, package manager, framework, or backend server. The application is contained in `index.html`.

## Repository Map

- `index.html` - Main application. Contains the HTML layout, Tailwind CDN config, custom CSS, and all JavaScript behavior.
- `README.md` - Human-facing project overview and local usage notes.
- `DESIGN.md` - Design system reference for colors, typography, spacing, component rules, and visual constraints.
- `.nojekyll` - Keeps GitHub Pages from running Jekyll processing.
- `ribbed_glass.jpg` - Local background texture used by the dashboard.
- `spiderman.png` - Local Spider-Man artwork backdrop used by the dashboard.
- `agent.md` - This guide for agents.

## Runtime And Deployment Model

This is a static site that can be opened directly in a browser or served by any static file server. GitHub Pages can host it from the repository root.

There are no install steps. Do not add `package.json`, bundlers, transpilers, or framework scaffolding unless the user explicitly asks for a larger architecture change.

Useful local check:

```bash
python -m http.server 8000
```

Then visit `http://localhost:8000`.

## Main Application Behavior

The dashboard currently includes:

- responsive bento-card layout
- dark default theme with light-theme toggle
- live clock and greeting
- reduced-motion-aware cursor canvas effect
- Pomodoro timer with focus and break modes
- audio player with playlist, volume, progress labels, and canvas visualizer
- AI news stream from TechCrunch RSS through `rss2json`
- practical fallback news cards when RSS loading fails
- local browser notes saved with `localStorage`
- local terminal-style command console

Important terminal commands in the UI:

- `/help`
- `/about`
- `/projects`
- `/skills`
- `/pomodoro start`
- `/pomodoro pause`
- `/pomodoro reset`
- `/notes`
- `/clear`

## External Browser Dependencies

The app depends on browser-accessible external services and CDNs:

- Tailwind CSS CDN: `https://cdn.tailwindcss.com`
- Google Fonts: Outfit, Plus Jakarta Sans, and Space Mono
- SoundHelix MP3 files for the audio player
- TechCrunch AI RSS feed through `https://api.rss2json.com`

When changing these integrations, keep failure states graceful. The dashboard should still load visually even if RSS, audio, fonts, or other network requests fail.

## Design Rules

Use `DESIGN.md` as the source of truth for visual direction.

Core design identity:

- theme: Spider-Man Miles Morales / Spider-Verse
- mood: tactical, energetic, premium, immersive
- primary accent: `#ff1722`
- default background: `#06070d`
- card surface: frosted translucent dark glass
- typography: Outfit for headings, Plus Jakarta Sans for body, Space Mono for technical labels
- layout rhythm: 8px spacing scale
- card shape: large squircle corners around `32px`

When editing UI:

- preserve the bento dashboard structure
- preserve crimson as the primary accent color
- keep cards translucent and glassy rather than solid blocks
- keep the default theme dark
- avoid introducing unrelated accent hues
- keep mobile and desktop layouts usable
- avoid breaking the backdrop images and canvas layers
- keep reduced-motion behavior intact

## Editing Guidelines For Agents

Because `index.html` contains markup, styles, and behavior together, make small focused edits and verify nearby interactions after changing anything.

Prefer these patterns:

- update existing CSS variables instead of scattering new hard-coded colors
- reuse `.bento-card`, `.card-content`, existing typography classes, and the crimson accent system
- keep widget JavaScript near the related existing section
- keep new browser state in `localStorage` only when persistence is expected
- create DOM nodes with `textContent` for fetched or user-controlled content
- keep user-facing text consistent with the tactical dashboard tone

Avoid these unless the user asks:

- adding a frontend framework
- adding a build step
- adding server-side code
- committing real API keys or tokens
- restoring browser-side Notion token sync through a public proxy
- replacing the Miles Morales visual direction

## Security And Privacy Notes

Notes are saved locally in the browser with `localStorage`. The previous Notion-style browser proxy sync is not part of the cleaned implementation because sending private API tokens through a public CORS proxy is not a safe default.

If the user asks for Notion sync later, prefer a small backend or serverless function that keeps tokens off the client.

## Verification Checklist

After changes, verify at minimum:

- page loads without console-breaking syntax errors
- layout works on desktop and mobile widths
- background images still render
- dark/light theme toggle works
- clock updates once per second
- Pomodoro start, pause, reset, and break mode work
- audio play/pause, previous/next, volume, and unavailable-track fallback work
- news section renders RSS items or fallback cards
- notes save and clear locally
- terminal commands listed in this file still work

For visual changes, also check:

- text does not overlap cards or controls
- cards keep the frosted glass style
- hover states still feel consistent
- crimson accent remains the dominant highlight

## Common Change Recipes

### Add A New Bento Card

Add a new `<section>` in the main grid, use the existing `bento-card` pattern, include a `card-content` child, and choose responsive grid spans that do not crowd the current layout.

### Add A Terminal Command

Update the terminal submit handler in `index.html`. Add the command to `/help`, handle arguments carefully, and keep responses short enough for the terminal panel.

### Change Dashboard Identity Text

Profile text, academic timeline, project names, and skills are hard-coded in `index.html`. Search for the visible text and update the nearby markup or terminal response together so the UI stays consistent.

### Change News Source

Edit `fetchAINews()`. Keep the fallback path through `renderBackupNews()` so the dashboard remains useful when the network or RSS parser fails.

### Change Audio Tracks

Edit the `tracks` array in `index.html`. Use browser-playable audio URLs and keep track names short enough for the compact card layout.

## Agent Defaults

When uncertain, preserve the current single-file static architecture, the design system in `DESIGN.md`, and the existing widget behavior. Make the smallest change that satisfies the user request, then verify the affected widget and nearby layout.
