# CLAUDE.md — HTML Prototype Playbook

> Standing instructions for building clickable HTML prototypes.
> Drop this file in the project root. Claude reads it automatically every session.
> **Per project:** only edit the `PROJECT` block and the `DESIGN TOKENS` block. Everything else stays.

---

## PROJECT

- **Client / industry:** Nimbus — B2B fleet-tracking & delivery-management SaaS for mid-sized logistics operators in Indonesia & Southeast Asia.
- **Goal of this prototype:** Clickable pitch prototype. NOT production code.
- **Core message / value prop:** Replace spreadsheets and WhatsApp check-ins with one live dashboard for end-to-end fleet visibility.
- **Primary CTA:** "Book a demo"
- **Sections (in order):** hero, trusted-by logos, problem→solution, core features, how-it-works, proof (stat + quote), final CTA, footer
- **Reference vibe:** Corporate, professional, structured, trustworthy. Calm enterprise software — big display type, generous whitespace, not busy.
- **Audience note:** Operations & fleet managers (20–200 vehicles). Non-technical, time-poor, skeptical of "another dashboard". Trust matters most — surface real-looking client logos and a hard metric early. Show the product (clean dashboard mockups), not abstract 3D illustrations. Mobile matters — they'll open the pitch link on their phone.

## ROLE & SCOPE

- My deliverable is the **prototype only**. Developers review and rebuild the code themselves later.
- Optimize for: **fast, visually convincing, clickable, responsive.** Do NOT over-engineer for production.
- Code just needs to be **readable enough that a developer understands intent** — semantic HTML, commented sections. No component framework, no build tooling unless I ask.

## TECH STACK

- Single `index.html`. Additional pages only if I ask.
- **Tailwind via CDN** for speed. Inline a small `<style>` block for tokens and custom bits.
- Vanilla JS for interactions. No UI frameworks (no React/Vue).
- **Animation libs via CDN are allowed and encouraged** for fluid motion: **Lenis** (smooth scroll) + **GSAP + ScrollTrigger** (scroll-driven reveals, parallax, counters). Load from cdnjs.
- Everything self-contained and deployable as static files (Vercel / Netlify).

## DESIGN TOKENS (single source of truth)

Define these as CSS variables at the top of `index.html` and reference them everywhere.
Never hardcode a color, size, or spacing value that isn't a token.

```css
:root {
  /* Color — Nimbus: navy + single amber accent */
  --color-bg:      #ffffff;
  --color-surface: #f6f7f9;
  --color-text:    #0f2a47;   /* deep navy */
  --color-muted:   #5b6b7c;
  --color-accent:  #f2a20c;   /* amber — CTAs & key data points ONLY */
  --color-border:  #e4e8ec;

  /* Type scale (1.25 ratio) */
  --text-xs:   0.8rem;
  --text-sm:   1rem;
  --text-base: 1.25rem;
  --text-lg:   1.563rem;
  --text-xl:   1.953rem;
  --text-2xl:  2.441rem;
  --text-3xl:  3.052rem;
  --text-hero: clamp(2.5rem, 6vw, 4.5rem);

  /* Spacing — 8pt grid */
  --space-1: 0.5rem;  --space-2: 1rem;   --space-3: 1.5rem;
  --space-4: 2rem;    --space-6: 3rem;   --space-8: 4rem;
  --space-12: 6rem;   --space-16: 8rem;  /* section padding */

  /* Radius / shadow — restrained */
  --radius: 0.5rem;
  --shadow: 0 1px 3px rgba(0,0,0,0.08);

  /* Type families */
  --font-display: 'Space Grotesk', system-ui, sans-serif;
  --font-body:    'Inter', system-ui, sans-serif;
}
```

> Load fonts via Google Fonts in `<head>`: Space Grotesk (display, 500/700) + Inter (body, 400/500). Both free for commercial use.

## VISUAL QUALITY BAR

- Whitespace is a feature. Generous section padding (`--space-16`), don't cram.
- Strong typographic hierarchy — size + weight carry the design, not decoration.
- Max 2 font families, max 2–3 weights.
- One accent color (amber), used sparingly (CTAs, key highlights/data points). Everything else navy/neutral.
- Alignment and rhythm: consistent max-width container, consistent vertical spacing between sections.
- Real, plausible copy — never lorem ipsum. Realistic lengths (a headline is 4–9 words, not 20).

## ANTI-AI-SLOP RULES (important — do NOT do these)

- ❌ No purple/blue gradient hero. No gradient text.
- ❌ No emoji in headings or as icons. Use a clean SVG icon set (inline) if icons are needed.
- ❌ No glassmorphism / heavy blur / neon glow.
- ❌ No over-rounded corners everywhere; no oversized drop shadows.
- ❌ No generic "Lorem ipsum" or "Company Name" placeholders — write real-sounding content.
- ❌ No three-identical-feature-cards-with-a-circle-icon unless it genuinely fits.
- ✅ Aim for something a senior designer would ship: restrained, confident, editorial.

## ANIMATION & MOTION (reference: ramp.com — fluid, refined, never flashy)

- **Smooth scroll with Lenis** on the whole page — that buttery inertial scroll is the biggest "premium" signal.
- **GSAP + ScrollTrigger** for scroll-driven motion: sections fade/slide up on enter, subtle parallax on hero/product visuals, count-up on key stats.
- **Easing is everything.** Use smooth `cubic-bezier` / GSAP `power2`/`power3` easing. Never linear. Enter animations ~0.6–0.9s, micro-interactions ~0.2–0.3s.
- **Animate only `transform` and `opacity`** (GPU-accelerated) so it stays 60fps. Never animate layout props (width/height/top/left/margin).
- **Restraint.** One idea per section, staggered gently. Motion should feel calm and confident like Ramp — not bouncy, not neon, no gimmicks.
- **Respect `prefers-reduced-motion`** — disable/soften animations for users who opt out.

## WORKFLOW RULES

- Build **one section at a time.** After each section, stop so I can review before continuing.
- Every section must be **responsive** (mobile-first; graceful stacking on small screens). Not desktop-only.
- Wire the tokens first, before building any section.
- Add micro-interactions in a final polish pass only: subtle hover states, smooth transitions, gentle scroll reveals. Keep them tasteful, never flashy.

## CODE CONVENTIONS

- Semantic HTML (`<header>`, `<section>`, `<nav>`, `<footer>`).
- Comment each section: `<!-- ===== HERO ===== -->`.
- Consistent, readable class patterns so a dev can port to components easily.
- No dead code, no unused CSS.

## COMMIT CONVENTIONS

- One commit per completed section or logical change — not one giant commit.
- Format: `type: short description` — `feat: hero section`, `style: refine services spacing`, `fix: mobile nav overflow`, `chore: initial scaffold`.
- Never commit secrets. `.env`, `node_modules/`, `.DS_Store`, `dist/` stay in `.gitignore`.

## HOW I'LL PROMPT

- Short prompts are fine — the rules above are assumed, don't ask me to repeat them.
- "Build the services section, 3 columns, follow the existing system" is a complete instruction.
- When I select code and ask for a change, apply it to that selection.
- Ask a clarifying question only when a choice would meaningfully change the outcome; otherwise pick the sensible default and note it.
