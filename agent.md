# Agent Guide

This file is for AI coding agents such as Codex, Claude Code, and similar tools working on this repository. It explains what the project is, how it is structured, and how to make changes safely.

## Project Summary

`My-personal-dashboard` is a static personal dashboard for Abhinav with a Miles Morales / Spider-Verse inspired visual system. It is designed as a high-contrast, frosted-glass bento dashboard with interactive widgets, local browser storage, and a few external browser-side integrations.

The project is intentionally compact. There is no build system, package manager, framework, or backend server in the repo. The application is mostly contained in one HTML file.

## Repository Map

- `index.html` - Main application. Contains the HTML layout, Tailwind CDN config, custom CSS, and all JavaScript behavior.
- `DESIGN.md` - Design system reference for colors, typography, spacing, component rules, and visual constraints.
- `.nojekyll` - Keeps GitHub Pages from running Jekyll processing.
- `ribbed_glass.jpg` - Local background texture used by the dashboard.
- `spiderman.png` - Local Spider-Man artwork backdrop used by the dashboard.
- `agent.md` - This guide for agents.

## Runtime And Deployment Model

This is a static site that can be opened directly in a browser or served by any static file server. GitHub Pages can host it from the repository root.

There are no install steps. Do not add `package.json`, bundlers, transpilers, or framework scaffolding unless the user explicitly asks for a larger architecture change.

Useful local checks:

```bash
# Option 1: open index.html directly in a browser

# Option 2: serve the repo with a simple static server
python -m http.server 8000
```

Then visit `http://localhost:8000`.

## Main Application Behavior

The dashboard currently includes:

- responsive bento-card layout
- dark default theme with light-theme toggle
- live clock and greeting
- animated cursor canvas with particle web effect
- Pomodoro timer with focus and break modes
- audio player with playlist, volume, progress labels, and canvas visualizer
- AI news stream from TechCrunch RSS through `rss2json`
- fallback news items when RSS loading fails
- Notion scratchpad dialog and sync flow
- local terminal-style command console

Important terminal commands in the UI:

- `/help`
- `/about`
- `/projects`
- `/skills`
- `/pomodoro start`
- `/pomodoro pause`
- `/pomodoro reset`
- `/notion`
- `/clear`

## External Browser Dependencies

The app depends on browser-accessible external services and CDNs:

- Tailwind CSS CDN: `https://cdn.tailwindcss.com`
- Google Fonts: Outfit, Plus Jakarta Sans, and Space Mono
- Avatar image from `https://ui-avatars.com`
- SoundHelix MP3 files for the audio player
- TechCrunch AI RSS feed through `https://api.rss2json.com`
- Notion page creation through `https://corsproxy.io/?https://api.notion.com/v1/pages`

When changing these integrations, keep failure states graceful. The dashboard should still load visually even if RSS, audio, avatar, fonts, or Notion requests fail.

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

## Editing Guidelines For Agents

Because `index.html` contains markup, styles, and behavior together, make small focused edits and verify nearby interactions after changing anything.

Prefer these patterns:

- update existing CSS variables instead of scattering new hard-coded colors
- reuse `.bento-card`, `.liquid-glass-shimmer`, `.btn-interactive`, and existing typography classes
- keep widget JavaScript near the related existing section
- keep new browser state in `localStorage` only when persistence is expected
- keep all user-facing text consistent with the current tactical dashboard tone

Avoid these unless the user asks:

- adding a frontend framework
- splitting the app into many files
- adding a build step
- adding server-side code
- committing real API keys or tokens
- replacing the Miles Morales visual direction

## Security And Privacy Notes

The Notion integration stores the token and database ID in browser `localStorage`. Agents must never add real Notion credentials to the repository.

If changing Notion behavior:

- keep token entry user-controlled
- do not hard-code secrets
- validate empty note, missing token, and missing database ID states
- preserve clear failure alerts or replace them with an equally visible UI state

The current browser-side Notion flow uses a public CORS proxy. Treat this as a convenience for a personal dashboard, not as a secure production pattern.

## Verification Checklist

After changes, verify at minimum:

- page loads without console-breaking syntax errors
- layout works on desktop and mobile widths
- background images still render
- dark/light theme toggle works
- clock updates once per second
- Pomodoro start, pause, reset, and break mode work
- audio play/pause, previous/next, and volume controls work
- news section renders RSS items or fallback items
- Notion dialog opens, closes, validates fields, and does not expose secrets
- terminal commands listed in this file still work

For visual changes, also check:

- text does not overlap cards or controls
- cards keep the frosted glass style
- hover states still feel consistent
- crimson accent remains the dominant highlight

## Common Change Recipes

### Add A New Bento Card

Add a new `<section>` in the main grid, use the existing `bento-card` pattern, include a `liquid-glass-shimmer` child, and choose responsive grid spans that do not crowd the current layout.

### Add A Terminal Command

Update the `handleTerminalCommand` switch in `index.html`. Add the command to `/help`, handle arguments carefully, and keep responses short enough for the terminal panel.

### Change Dashboard Identity Text

Profile text, academic timeline, project names, and skills are hard-coded in `index.html`. Search for the visible text and update the nearby markup or terminal response together so the UI stays consistent.

### Change News Source

Edit `fetchAINews()`. Keep the fallback path through `renderBackupNews()` so the dashboard remains useful when the network or RSS parser fails.

### Change Audio Tracks

Edit the `playlist` array in `index.html`. Use browser-playable audio URLs and keep track names short enough for the compact card layout.

## Agent Defaults

When uncertain, preserve the current single-file static architecture, the design system in `DESIGN.md`, and the existing widget behavior. Make the smallest change that satisfies the user request, then verify the affected widget and nearby layout.
