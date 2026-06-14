# Synapse AI LLC — Website Design Spec

## Overview

A single-page static website for Synapse AI LLC, hosted on GitHub Pages with a custom domain (`synapse-ai.biz`) managed via Cloudflare DNS. The site serves as a minimal digital presence with a stealth AI startup aesthetic.

## Domain & Infrastructure

- **Domain:** `synapse-ai.biz` (registered on Cloudflare)
- **DNS:** CNAME record pointing to `get-synapse-ai.github.io` via `flarectl`
- **Hosting:** GitHub Pages on repo `get-synapse-ai/synapse-ai-website` (org: `get-synapse-ai`)
- **CNAME file:** `synapse-ai.biz` in repo root for GitHub Pages custom domain

## Visual Design

### Aesthetic

- Dark theme, near-black background (`#00000a`)
- Monospace typography (Share Tech Mono, Syncopate)
- Stealth AI startup vibe: mysterious, minimal, alive
- Scanline overlay and vignette for texture

### Background — 3D Neural Synapse Visualization

A non-interactive Three.js 3D neuron rendered on a full-viewport canvas behind the page content. Adapted from the user's reference implementation:

- **Geometry:** Procedural neuron — icosahedron soma with CatmullRom curve dendrites and branching axons
- **Rendering:** Custom GLSL vertex/fragment shaders with noise-based texturing, Fresnel rim lighting, and pulse/activation color effects
- **Post-processing:** UnrealBloomPass for glow
- **Particles:** Three layers of dust particles with additive blending
- **Auto-fire:** The neuron fires automatically on a random interval (8-15 seconds). No user interaction — no click handler, no custom cursor
- **Camera:** Slow auto-rotation via simple animation (no OrbitControls). Camera is fixed; user cannot interact with the 3D scene
- **Canvas:** `pointer-events: none`, `z-index: 0`, sits behind all content
- **Overlays:** Vignette gradient and scanline repeating-gradient overlays (from reference)

### Foreground — Page Content

Centered vertically and horizontally over the neuron background:

1. **Company name:** `SYNAPSE AI` — large, Share Tech Mono or Syncopate, with subtle cyan text-shadow glow
2. **Tagline:** `bespoke machine intelligence. san francisco.` — smaller, muted color, with CSS blinking cursor animation. Deliberately lowercase and terse
3. **Spacer:** generous whitespace
4. **Contact:** `> contact@synapse-ai.biz` — mailto link in cyan accent color, terminal-prompt style

No navigation, no footer, no hamburger menu.

## Tech Stack

- Single `index.html` file
- **Three.js** + addons (OrbitControls removed, EffectComposer/RenderPass/UnrealBloomPass kept) via CDN importmap (`cdn.jsdelivr.net/npm/three@0.170.0`)
- **Tailwind CSS** via CDN for text layout and responsive utilities
- **Google Fonts:** Share Tech Mono, Syncopate
- **CSS animations:** Blinking cursor, scanline/vignette overlays
- **No build step**, no JS framework, no bundler

## Removed from Reference

These elements from the user's reference are explicitly excluded:

- Custom cursor (`#cursor` element and `cursor: none`)
- UI telemetry panel (`#ui-panel` with membrane voltage, dendrite count, etc.)
- Coordinate display (`#coords`)
- Corner brackets (`.corner` elements)
- Click-to-fire interaction (replaced with automatic random-interval firing)
- OrbitControls (replaced with simple auto-rotation in the animation loop)

## Files

```
synapse-ai-website/
├── index.html    # The entire website
├── CNAME         # synapse-ai.biz (for GitHub Pages)
└── README.md     # (optional)
```

## Deployment Steps

1. Create GitHub repo `get-synapse-ai/synapse-ai-website` via `gh repo create` under the org
2. Add `index.html` and `CNAME`
3. Configure GitHub Pages via `gh api` to serve from main branch root
4. Add Cloudflare DNS CNAME record via `flarectl`: `synapse-ai.biz` → `get-synapse-ai.github.io`
