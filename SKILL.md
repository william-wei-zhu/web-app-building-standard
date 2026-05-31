---
name: web-app-building-standard
description: "William's standard for building web apps: simplicity-first, large & high-contrast type, logo + tagline branding, pagination, minimal OG image, required privacy page, and a fixed stack (Vercel, Google Cloud, Gemini, GitHub, Exa, PostHog). Apply on every website/web-app build."
version: 1.1.0
license: MIT
metadata:
  hermes:
    tags: [web, frontend, design, ui, ux, accessibility, branding, nextjs, tailwind, vercel, standards, simplicity]
    related_skills: []
    homepage: https://github.com/william-wei-zhu/web-app-building-standard
---

# William's Web App Building Standard

A reusable standard for building small, polished public web apps. It exists so the same refinements don't have to be re-requested on every new project. **Apply these by default; deviate only with a stated reason.** Defaults below are adaptable baselines (the [pbcindex](https://pbcindex.com) site is the reference implementation), not the only valid choices.

The single most important rule: **simplify**.

> Note to self: do not use em-dashes anywhere in this project's writing. Use a comma, colon, period, semicolon, or "and / but / so" instead.

---

## Workflow: start from the core, then build outward

Every project starts from a **pain point**. Before building any UI, nail the core identity **in this order**. The rest of the site is built entirely on top of it:

1. **Pain point**: the specific problem this app solves, and for whom.
2. **Web domain**: secure it.
3. **Company / product name.**
4. **Logo.**
5. **Tagline.**
6. **Mission statement.**

Only once these are settled do you build out the rest (pages, features, data), all derived from them. The **tagline** drives the hero, tab title, and OG image; the **logo** drives the header, favicon, and OG; the **mission** drives the about page and the site's voice. If a later decision feels arbitrary, return to the core and derive it.

---

## 1. First principle: simplicity ("Simpli-T")

Default to **removing, not adding**. When unsure, ship the plainer version.

- Cut decorative text, stat strips, eyebrows, sequence numbers (e.g. `001` / `002`), redundant labels, and any chrome that doesn't earn its place.
- Every screen and asset must pass one test: **"What can be removed?"**
- Prefer one strong element over three weak ones. White space is a feature.

## 2. Typography & sizing

Big and legible. Design as if for an older reader ("easy for my grandma to read").

- **Global zoom ~120%** (e.g. `html { font-size: 120% }`) so all rem-based type and spacing scale up uniformly.
- Bump the type scale: body ≈ **1.2rem**, with a generous body line-height (~**1.7**).
- **Fonts are principles, not fixed faces.** Choose per project, but always include:
  - a **characterful display face** for headings (a serif with personality works well),
  - a **highly readable body face** (editorial serif or a clean sans),
  - a **monospace** for data, labels, and small-caps eyebrows (uppercase, tracked ~0.16em).
- No tiny text. If a label feels small, it's too small.

## 3. Color & contrast (accessibility)

High contrast, **"all black or all white"**, never faded gray text.

- Use **solid foreground** on background. **No opacity grays** for text (avoid `text-foreground/70`, etc.).
- Secondary/muted text uses a **near-ink (light theme) / near-paper (dark theme)** token, not a transparent foreground.
- **One accent color**, used sparingly (links, key emphasis, a single rule). Headings use ink, not the accent.
- Verify both themes read cleanly.

## 4. Theme (light + dark)

- Ship both, via a class-based theme provider (e.g. `next-themes`, `attribute="class"`), **defaulting to the system theme** (`defaultTheme="system"`).
- A small toggle lives in the header.
- High-contrast in both modes: light = near-black on white; dark = near-white on near-black.

## 5. Brand: logo & tagline

Every site has a **logo** and a **tagline**.

- **Logo** is used everywhere it belongs: header, favicon (`icon.png`), apple touch icon, and the OG image. Keep a vector source in the repo. Size it up, but on mobile it must never crowd the nav (hide a redundant text wordmark below the `sm` breakpoint when the logo already contains the name).
- **Tagline**: one elegant line with **italic accent emphasis** on the key phrase. The tagline is also the **browser tab title** and the **OG/Twitter title**.

## 6. Layout & navigation

- **Pagination** on any long list: ~**12 per page**, `Prev · 1 2 3 … · Next`. Reset to page 1 when filters change, smooth-scroll to the list top on page change, and show the visible range (e.g. "01–12 of 45").
- **Header is NOT sticky**: it scrolls away with the page (don't freeze it at the top).
- **Mobile layout optimization is non-negotiable.** A desktop layout shrunk down is not a mobile layout. Take a real screenshot at ~**375 to 390px** and fix it before shipping. Check each item:
  - [ ] **No horizontal overflow or scrollbar.** Nothing clips at the right edge.
  - [ ] **Scale display headings down on mobile** (responsive type, e.g. `text-4xl sm:text-7xl`). Hero headings sized for desktop overflow on phones.
  - [ ] **No forced no-wrap in headings.** Avoid non-breaking spaces (`&nbsp;`) and `whitespace-nowrap` on long phrases; they push text off-screen instead of letting it wrap.
  - [ ] **Gate typographic flourishes to `sm` and up.** Drop caps, oversized first letters, and very tight leading crowd a narrow column; show them only on wider screens.
  - [ ] **Stack multi-column rows into one column on mobile.** A `justify-between` two-column row (footer credits, split nav) reads as two disconnected blocks on a phone.
  - [ ] **Trim oversized vertical padding** so the hero does not push the real content below the fold.
  - [ ] **Tap targets are comfortably large** (~44px) and not crowded together.
  - [ ] **The header logo never crowds the nav** (hide a redundant text wordmark below the `sm` breakpoint when the logo already contains the name).

## 7. Required pages

- A **privacy / disclaimer page**: "informational only, not legal/professional advice; verify before relying."
- An **about / methodology page** explaining what the site is and how it works.
- A **footer** with attribution **"Built by William Zhu"** linking `https://www.linkedin.com/in/william-wei-zhu/`, plus any license/legal links.

## 8. Social / OG preview image

- **Minimal: logo + tagline only.** No counts, eyebrows, or decorative pills.
- Standard **1200×630**, generated at build (e.g. `next/og`).
- Remember: platforms **cache** OG cards. Refresh via their debugger or a throwaway `?v=` query string.

## 9. Writing & voice

- **No em-dashes.** Use a comma, colon, period, semicolon, or "and / but / so" instead.
- **No specific company names** in placeholders or examples; use generic phrasing.
- Plain, confident copy for a non-technical reader.

## 10. Process: design & security

- Build distinctive UI with the **`frontend-design` skill** to avoid generic AI aesthetics.
- Before shipping, run a **security check** (the `security-review` skill) over the diff:
  - secrets stay in **gitignored** env files, never committed;
  - auth / admin routes are gated;
  - public endpoints have **rate limiting + bot protection**;
  - all user input is validated.

## 11. Stack (defaults)

| Concern | Default |
|---|---|
| Host + deploy | **Vercel** (deploy via CLI) |
| Data | **Google Cloud** (Firestore) |
| AI | **Gemini via Vertex AI**, the fastest model (currently 3.1 Flash Lite) |
| Version control | **GitHub** (public repos by default unless data-sensitive) |
| Research / search | **Exa** |
| Product analytics | **PostHog** (wire on launch) |
| Email | **Resend** (transactional email + email auth / magic links, when a project needs them) |
| Framework | **Next.js (App Router) + Tailwind v4 + shadcn/ui** |

Workflow: **commit + push every change** (all files, not just task-related ones), and keep `CLAUDE.md` / docs in sync with code.

## 12. Standard build checklist

Apply these up front, before being asked:

- [ ] Core identity defined first: pain point, domain, name, logo, tagline, mission
- [ ] Logo + tagline in place
- [ ] Big fonts (~120% base), generous line-height
- [ ] Solid high-contrast color, no gray text
- [ ] Simplify / remove anything unnecessary
- [ ] Pagination on long lists (~12/page)
- [ ] Header not sticky
- [ ] Logo sized up, no mobile overlap
- [ ] Minimal logo + tagline OG image
- [ ] System-default light/dark toggle
- [ ] Tagline set as tab title + OG title
- [ ] Privacy / disclaimer page
- [ ] "Built by William Zhu" footer + LinkedIn
- [ ] **Mobile layout optimized + verified at 375 to 390px** (no overflow, headings scaled down, no `&nbsp;` clipping, flourishes gated to `sm+`, multi-column rows stacked); see section 6
- [ ] Built UI with `frontend-design` skill
- [ ] `security-review` run before shipping
- [ ] No em-dashes, no company names
- [ ] Stack: Vercel · Google Cloud · Gemini · GitHub · Exa · PostHog · Resend (email/auth, when needed)
- [ ] Committed, pushed, deployed, docs updated

## 13. How to work with William (note to the agent)

- He iterates **visually** and asks **"what do you think?"**: give a real **recommendation with trade-offs**, not just a menu of options. Lead with the recommendation, then act.
- He asks **"where is X / how do I access it?"**: answer with the **exact URL and any credentials**.
- He **favors deleting over adding**. When in doubt, cut.
