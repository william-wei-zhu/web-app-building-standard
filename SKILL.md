---
name: web-app-building-standard
description: "William's standard for building web apps: simplicity-first, large & high-contrast type, logo + tagline branding, pagination, minimal OG image, required privacy page, an optional hidden technical walk-through page, and a fixed stack (Vercel, Google Cloud, Gemini, GitHub, Exa, PostHog). Apply on every website/web-app build."
version: 1.6.0
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

## 0. When this standard yields: cloning a target brand

This standard is opinionated, but it is **not** meant to override deliberate brand mimicry. When the goal is for an app to look native to a specific existing product or company (for example, a tool built to feel like it was made by Exa, Stripe, or Linear, often for a demo, take-home, or partner-facing build), **fidelity to that target brand wins** over this standard's own visual conventions.

In that mode:

- **Use the target's real assets and system, do not invent.** Their actual logo, header, footer, fonts, colors, radii, and layout patterns. Lift them from a real reference (e.g. the target's site or an existing on-brand build) rather than approximating.
- These visual rules **defer to the target**: the logo rules (§5), light/dark + system theme (§4), non-sticky header (§6), the ~120% type scale (§2), and the OG "logo only" image (§9) all bend to match the target instead.
- **What still holds, always:** the core identity workflow (§0-adjacent: pain point → domain → name → tagline → mission), simplicity (§1), mobile optimization and the 375-390px pass (§6), the required pages and "Built by William Zhu" attribution (§7), writing voice incl. no em-dashes (§10), security review + secrets hygiene (§11), the stack defaults (§12), and shipping/commit discipline (§13). Accessibility *intent* (legible, high-contrast) holds even when the exact tokens come from the target.
- **Record the deviation.** Note in the project's `CLAUDE.md` that the frontend intentionally clones brand X and which conventions it overrides, so it reads as a decision, not a drift.

Reference implementation: [exavantage.com](https://exavantage.com) (Exa Vantage), an FSI research tool deliberately skinned as Exa (real Exa logo, header, footer, fonts, palette) while keeping the rest of this standard.

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
- **Never, ever use a left-border accent-bar.** Do not put a colored vertical bar on the left edge of cards, callouts, blockquotes, list items, or section headers (e.g. `border-l-4 border-accent`, the classic "colored stripe down the side" treatment). It is a generic AI-template tell and it is banned outright. To set content apart, use whitespace, a full hairline border, a subtle background, or weight and size instead.
- Verify both themes read cleanly.

## 4. Theme (light + dark)

- Ship both, via a class-based theme provider (e.g. `next-themes`, `attribute="class"`), **defaulting to the system theme** (`defaultTheme="system"`).
- A small toggle lives in the header.
- High-contrast in both modes: light = near-black on white; dark = near-white on near-black.

## 5. Brand: logo & tagline

Every site has a **logo** and a **tagline**.

- **Logo** is used everywhere it belongs: header, favicon (`icon.png`), apple touch icon, and the OG image. Keep a vector source in the repo. Size it up, but on mobile it must never crowd the nav (hide a redundant text wordmark below the `sm` breakpoint when the logo already contains the name).
- **Tagline**: one elegant line with **italic accent emphasis** on the key phrase. It anchors the hero and the **browser tab title**. In the social card it is the **OG/Twitter description**, with the **app name as the OG/Twitter title** (see §8).

## 6. Layout & navigation

- **Pagination** on any long list: ~**12 per page**, `Prev · 1 2 3 … · Next`. Reset to page 1 when filters change, smooth-scroll to the list top on page change, and show the visible range (e.g. "01–12 of 45").
- **Header is NOT sticky**: it scrolls away with the page (don't freeze it at the top).
- **Mobile layout optimization is non-negotiable.** A desktop layout shrunk down is not a mobile layout. Take a real screenshot at ~**375 to 390px** and fix it before shipping. Check each item:
  - [ ] **No horizontal overflow or scrollbar.** Nothing clips at the right edge.
  - [ ] **Scale display headings down on mobile** (responsive type, e.g. `text-4xl sm:text-7xl`). Hero headings sized for desktop overflow on phones.
  - [ ] **No forced no-wrap in headings.** Avoid non-breaking spaces (`&nbsp;`) and `whitespace-nowrap` on long phrases; they push text off-screen instead of letting it wrap.
  - [ ] **Gate typographic flourishes to `sm` and up.** Drop caps, oversized first letters, and very tight leading crowd a narrow column; show them only on wider screens.
  - [ ] **Stack multi-column rows into one column on mobile.** A `justify-between` two-column row (footer credits, split nav) reads as two disconnected blocks on a phone.
  - [ ] **Long control rows must not overflow.** Pagination, toolbars, and tab strips grow as content grows. Let them wrap (`flex-wrap justify-center`) and shrink controls on mobile (e.g. icon-only Prev/Next), so a `justify-between` row never pushes a button off the right edge (which adds blank horizontal scroll space).
  - [ ] **Trim oversized vertical padding** so the hero does not push the real content below the fold.
  - [ ] **Tap targets are comfortably large** (~44px) and not crowded together.
  - [ ] **The header logo never crowds the nav** (hide a redundant text wordmark below the `sm` breakpoint when the logo already contains the name).

## 7. Required pages

- A **privacy / disclaimer page**: "informational only, not legal/professional advice; verify before relying."
- An **about / methodology page** explaining what the site is and how it works.
- A **footer** with attribution **"Built by William Zhu"** linking `https://www.linkedin.com/in/william-wei-zhu/`, plus any license/legal links.

## 8. The technical walk-through page (optional, hidden)

A single **unlisted** page that explains, in plain language with visuals, **exactly what happens when a user performs the core action**. It exists for demos, interviews, portfolio reviewers, and curious stakeholders: people who need to understand the system without reading the code. Add it when explaining the app clearly is worth it (showing the work to a prospective employer, say); skip it for a purely utilitarian tool.

**Hidden by default.** Reachable only by typing the URL.
- `robots: { index: false, follow: false }`, and keep it out of `sitemap.ts`.
- **Not linked** from header, footer, or home.
- **No password needed**, because the page documents architecture only and shows **zero secrets** (no keys, tokens, or private values). Add a light gate only if it must expose something sensitive.
- A short, memorable path is fine (e.g. `/docs`); it leaks nothing.

**Two audiences at once.** Lead with plain language a non-technical reader follows, but **name the real components and their exact features** so an engineer respects it. Not "an AI model" but the model id and provider; not "search" but the specific search product and its parameters. Both audiences read the same page.

**Shape it for few words, lots of visuals:**
- A one-line summary of the whole flow up top.
- A visual **end-to-end overview** (the pipeline at a glance).
- The journey as a handful of **steps / "acts"**, each one **a single illustration plus a few words**, with a precise one-line technical caption.
- A compact **"what it runs on"** layer naming exact features.
- Optional **"notes for engineers"**: the few non-obvious decisions that show real depth.

**Visuals match the brand, with no new dependencies.**
- **Hand-build** the diagrams and illustrations in **SVG / CSS** using the site's own tokens (fonts, accent, borders). Do **not** drop in stock photos or a charting / diagram library (Mermaid, D3); they fight the brand and add weight.
- Motion is **refined and one-shot**: elements fade or draw themselves in **once** as they scroll into view. **No auto-looping.** Always honor `prefers-reduced-motion`.
- Verify it in light, dark, and at 375 to 390px like any other page (§6).

**Accuracy is the whole point.**
- Document the **real** stack and the **real** parameters (model ids, the exact search product and options, thresholds, timeouts, rate limits). Wrong details lose the technical audience instantly.
- **Never put a secret on the page.** Architecture only.
- Treat it as living: when the pipeline changes, update the page.

## 9. Social / OG preview link

The card has two parts: the **image** and the **share text** under it. Keep the words out of the image and in the text.

**The image:**
- **Logo only, no text at all.** No app name, tagline, counts, eyebrows, or decorative pills baked into the image.
- **Make the logo really large**, sized to fill the frame height with only a small margin. A bold, oversized mark reads best as a thumbnail in a feed.
- Use a **high-resolution logo source** (e.g. 1024px square) so it stays crisp when scaled up.
- Standard **1200×630**, generated at build (e.g. `next/og`), on the brand background.

**The share text (this is where the words go):**
- **OG / Twitter title = the app name** (e.g. "SkatePuck").
- **OG / Twitter description = the tagline** (e.g. "Skate to where your market is going.").
- The platform renders the title bold with the description beneath, so the words never belong inside the image.

**Implementation:**
- Define the preview at the **site root**, not only on dynamic subpages. If only subpages have an OG image, sharing the homepage renders no preview at all (a common bug).
- Set a **`metadataBase`** so image URLs resolve to absolute `https://` URLs.
- Provide **both** `opengraph-image` and `twitter-image` (App Router file conventions) and use `summary_large_image` for Twitter/X.
- Remember: platforms **cache** OG cards. Refresh via their debugger (e.g. LinkedIn Post Inspector) or a throwaway `?v=` query string.

## 10. Writing & voice

- **No em-dashes.** Use a comma, colon, period, semicolon, or "and / but / so" instead.
- **No specific company names** in placeholders or examples; use generic phrasing.
- Plain, confident copy for a non-technical reader.

## 11. Process: design & security

- Build distinctive UI with the **`frontend-design` skill** to avoid generic AI aesthetics.
- Before shipping, run a **security check** (the `security-review` skill) over the diff:
  - secrets stay in **gitignored** env files, never committed;
  - auth / admin routes are gated;
  - public endpoints have **rate limiting + bot protection**;
  - all user input is validated.

## 12. Stack (defaults)

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

## 13. Standard build checklist

Apply these up front, before being asked:

- [ ] Core identity defined first: pain point, domain, name, logo, tagline, mission
- [ ] Logo + tagline in place
- [ ] Big fonts (~120% base), generous line-height
- [ ] Solid high-contrast color, no gray text
- [ ] No left-border accent-bars anywhere (no `border-l` accent stripes on cards/callouts/blockquotes)
- [ ] Simplify / remove anything unnecessary
- [ ] Pagination on long lists (~12/page)
- [ ] Header not sticky
- [ ] Logo sized up, no mobile overlap
- [ ] OG image: logo only, sized really large to fill the frame (no text)
- [ ] OG/Twitter title = app name, description = tagline; preview defined at the site root (both `opengraph-image` + `twitter-image`)
- [ ] System-default light/dark toggle
- [ ] Tagline set as tab title
- [ ] Privacy / disclaimer page
- [ ] (If a demo / portfolio matters) Hidden technical walk-through page: unlisted + `noindex`, not linked anywhere, few words + on-brand SVG visuals, names the real stack, shows no secrets
- [ ] "Built by William Zhu" footer + LinkedIn
- [ ] **Mobile layout optimized + verified at 375 to 390px** (no overflow, headings scaled down, no `&nbsp;` clipping, flourishes gated to `sm+`, multi-column rows stacked); see section 6
- [ ] Built UI with `frontend-design` skill
- [ ] `security-review` run before shipping
- [ ] No em-dashes, no company names
- [ ] Stack: Vercel · Google Cloud · Gemini · GitHub · Exa · PostHog · Resend (email/auth, when needed)
- [ ] Committed, pushed, deployed, docs updated

## 14. How to work with William (note to the agent)

- He iterates **visually** and asks **"what do you think?"**: give a real **recommendation with trade-offs**, not just a menu of options. Lead with the recommendation, then act.
- He asks **"where is X / how do I access it?"**: answer with the **exact URL and any credentials**.
- He **favors deleting over adding**. When in doubt, cut.
