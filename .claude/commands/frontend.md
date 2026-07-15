---
allowed-tools: Read, Glob, LS
description: Generate distinctive, non-generic frontend UI. Applies the full aesthetics prompt — typography, color, motion, backgrounds — to avoid AI slop defaults. Use for any UI generation task.
---

# /frontend — Frontend Aesthetics Mode

You are now in **FRONTEND AESTHETICS MODE**. The full aesthetics system prompt is active.

## Task
$ARGUMENTS

---

## MANDATORY AESTHETICS RULES (read before writing a single line of CSS)

<frontend_aesthetics>
You tend to converge toward generic, "on distribution" outputs. In frontend design, this creates what users call the "AI slop" aesthetic. Avoid this: make creative, distinctive frontends that surprise and delight. Focus on:

**Typography:** Choose fonts that are beautiful, unique, and interesting. Avoid generic fonts like Arial and Inter. Opt for distinctive choices that elevate the frontend's aesthetics.

**Color & Theme:** Commit to a cohesive aesthetic. Use CSS variables for consistency. Dominant colors with sharp accents outperform timid, evenly-distributed palettes. Draw from IDE themes and cultural aesthetics for inspiration.

**Motion:** Use animations for effects and micro-interactions. Prioritize CSS-only solutions for HTML. Use Motion library for React when available. Focus on high-impact moments: one well-orchestrated page load with staggered reveals (animation-delay) creates more delight than scattered micro-interactions.

**Backgrounds:** Create atmosphere and depth rather than defaulting to solid colors. Layer CSS gradients, use geometric patterns, or add contextual effects that match the overall aesthetic.

**Avoid generic AI-generated aesthetics:**
- Overused font families (Inter, Roboto, Arial, Open Sans, Lato, system fonts)
- Clichéd color schemes (particularly purple gradients on white backgrounds)
- Predictable layouts and component patterns
- Cookie-cutter design that lacks context-specific character
- Space Grotesk (overused across AI-generated outputs — avoid unless specifically fitting)

Interpret creatively and make unexpected choices that feel genuinely designed for the context. Vary between light and dark themes, different fonts, different aesthetics.

It is critical that you think outside the box.
</frontend_aesthetics>

---

## FONT SELECTION GUIDE

**Never use:** Inter, Roboto, Arial, Open Sans, Lato, default system fonts, Space Grotesk (unless isolated Typography mode)

**High-impact choices by aesthetic:**

| Aesthetic | Font choices |
|---|---|
| Code / technical | JetBrains Mono, Fira Code, IBM Plex Mono |
| Editorial / premium | Playfair Display, Crimson Pro, Fraunces, Newsreader |
| Startup / product | Clash Display, Satoshi, Cabinet Grotesk, Bricolage Grotesque |
| Technical / clean | IBM Plex Sans, Source Sans 3 |
| Distinctive | Obviously, Bricolage Grotesque, Instrument Serif |

**Pairing principle:** High contrast = interesting.
- Display + monospace
- Serif + geometric sans
- Variable font used across its weight extremes (100 vs 900, not 400 vs 600)

**Size extremes:** Use 3x+ size jumps, not 1.5x. A hero at 96px paired with body at 16px reads as designed. 32px vs 20px reads as accidental.

Load fonts from Google Fonts. State your font choice before writing CSS.

---

## COLOR APPROACH

Pick one dominant color, one or two supporting colors, one sharp accent. Do not distribute colors evenly — hierarchize them.

**Inspiration sources:**
- IDE themes: Dracula, Catppuccin, Tokyo Night, Gruvbox, Nord, Monokai
- Cultural aesthetics: brutalism, Swiss design, vaporwave, solarpunk, cyberpunk, art nouveau
- Material: concrete, glass, paper, metal, fabric

**Avoid:**
- Purple + white (the default AI output)
- Gradients that go from one saturated color to another saturated color
- 5+ colors with no hierarchy

---

## TECH STACK DEFAULTS

Unless the task specifies otherwise:
- **HTML tasks:** Vanilla HTML + CSS + JS, Tailwind via CDN for utilities
- **React tasks:** React + Tailwind, Motion library for animations
- **Vue tasks:** Vue 3 + Tailwind (matches Securacy stack)

Generate complete, self-contained code. All CSS and JS inline for HTML outputs.

---

## ISOLATED MODE (when user specifies a single dimension)

If the user says "typography only", "color only", or specifies a theme — apply only that dimension, don't override others.

**Typography only prompt active when:** user says "font", "typography", "just improve the type"
→ Apply font guidance only. Leave colors, motion, backgrounds untouched.

**Theme constraint active when:** user specifies a named aesthetic (solarpunk, brutalist, etc.)
→ Lock that theme. Apply all four dimensions through its lens.

---

## BEFORE WRITING ANY CODE

State your design decisions explicitly:
1. **Font chosen:** [name] — why it fits this context
2. **Color approach:** [dominant] + [accent] — inspiration source
3. **Motion plan:** [what animates, when, how]
4. **Background treatment:** [approach]

Then write the code. This forces deliberate choices instead of defaults.