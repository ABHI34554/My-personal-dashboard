---
name: Miles Morales Bento OS
version: 1.1
theme: Spider-Man Miles Morales
colors:
  primary: "#ff1722"      # Spider Crimson
  secondary: "#121214"    # Carbon Grey
  accent: "#ff1722"       # Web Glow Accent
  neutral: "#64748b"      # Muted slate
  background: "#06070d"   # Deep Void Space
  surface: "rgba(10, 11, 20, 0.55)" # Frosted glass surface
  border: "rgba(255, 23, 34, 0.08)"  # Crimson-highlighted border
  text: "#f8fafc"         # Off-white
typography:
  fontFamily:
    headings: "Outfit"
    body: "Plus Jakarta Sans"
    mono: "Space Mono"
  fontWeight:
    headings: 800
    body: 500
spacing:
  sm: "8px"
  md: "16px"
  lg: "24px"
  xl: "32px"
rounded:
  sm: "8px"
  md: "16px"
  lg: "32px"              # Squircle panels
shadows:
  sm: "0 2px 8px rgba(0, 0, 0, 0.2)"
  md: "0 8px 30px rgba(0, 0, 0, 0.4)"
  lg: "0 0 20px rgba(255, 23, 34, 0.25)" # Neon red glowing drop shadow
---

# Design System — Miles Morales Bento OS

## Design Philosophy & Personality
This design is a street-art inspired, tech-forward, high-contrast dashboard mimicking the visual environment of Spider-Man: Into the Spider-Verse. The visual tone is tactical, energetic, and premium.
- **Personality traits**: Tactical, Energetic, Premium, Immersive

## Usage Guidelines
- **Colors**: Use `primary` (#ff1722) for highlight indicators, active buttons, and visual focus. Use the frosted-glass `surface` for panels, and the deep `background` (#06070d) to anchor the canvas.
- **Typography**: Apply Outfit for bold headers to emphasize titles, and Plus Jakarta Sans for body content to ensure accessibility.
- **Spacing**: Align layouts strictly to an 8px grid (8, 16, 24, 32px values).

## Component Design Guidelines
- **Bento Cards**: Panels use smooth squircle corners (`rounded-lg` / 32px), translucent gradient border masks, and subtle neon red glowing drop shadows on hover.
- **Top Layer dialogs**: Modals use native `<dialog>` tags with frosted backdrops and smooth fade transitions.
- **Text inputs**: Forms use fluid, content-fitting heights (`field-sizing: content`) and show validation error rings only after interaction (`:user-invalid`).

## What to Avoid (Don'ts)
- Do not use bright, saturated solid backgrounds for large card structures. Keep them frosted and semi-transparent.
- Avoid using standard square corners. Everything must fit the squircle layout.
- Do not mix color hues for accent markers. Stick exclusively to the Spider Crimson (#ff1722).
