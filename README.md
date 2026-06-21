# William's Web App Building Standard

A reusable standard for building small, polished public web apps, so the same design and build decisions don't have to be re-made (or re-requested) on every new project.

It is opinionated by design. The guiding rule is **simplify**: large, high-contrast type; a clean logo + tagline; only the pages that earn their place; and a fixed, boring-on-purpose stack. Projects start from a **pain point**, then a core identity (domain, name, logo, tagline, mission), and everything else is built on top of that.

The full standard lives in **[`SKILL.md`](./SKILL.md)**.

## What it covers

- **Workflow**: start from the core (pain point, domain, name, logo, tagline, mission), then build outward
- **Brand-cloning override**: when an app is meant to look native to a target brand (e.g. built to feel like it's made by Exa), fidelity to that brand wins over the standard's own visual conventions; the rest of the standard still applies
- **Simplicity first**: remove before you add
- **Typography**: large and legible (~120% base), fonts as principles not fixed faces
- **Color & contrast**: all black or all white, no gray text; no accent bar on any edge (left or top); consistent thin-border cards and one light callout style
- **Composition & hierarchy**: lead-with-the-conclusion headlines, one focal point per view, design to the frame for fixed-format artifacts, refined one-shot motion (reduced-motion honored)
- **Theme**: light + dark, system default
- **Brand**: logo and tagline, everywhere they belong
- **Layout**: pagination, non-sticky header, mobile layout optimization (verified at 375 to 390px: responsive headings, no `&nbsp;` clipping, flourishes gated to `sm+`, rows stacked)
- **Inputs & states**: validate early with a high-precision guard, plus designed empty / loading / error / invalid states with one-tap example inputs
- **Generated-content apps**: honesty (cite or omit, label estimates, verifiable claims), prompt-injection defense, determinism, model-tier-to-the-job
- **Cost & resilience**: per-IP rate limit + global budget kill switch, caching, graceful degradation; destructive scripts dry-run by default
- **Required pages**: privacy/disclaimer, about, "Built by William Zhu" footer
- **Technical walk-through (optional, hidden)**: an unlisted, `noindex` page that explains what happens behind the scenes, in plain language plus on-brand SVG visuals, naming the real stack and showing no secrets
- **Social preview**: image is the logo only, sized really large (no text); title = app name, description = tagline; defined at the site root
- **Process**: `frontend-design` for UI, `security-review` before shipping
- **Stack**: Vercel · Google Cloud · Gemini · GitHub · Exa · PostHog · Resend · Next.js + Tailwind + shadcn/ui

## How to use it

1. **Reference it from a project.** Add a line to the project's `CLAUDE.md`:
   > UI/UX and build conventions follow William's Web App Building Standard:
   > https://github.com/william-wei-zhu/web-app-building-standard
2. **Use it as an agent skill.** Drop `SKILL.md` into your skills directory (e.g. `~/.hermes/skills/software-development/web-app-building-standard/SKILL.md`) so it activates on web/frontend work.
3. **Read it directly.** Open [`SKILL.md`](./SKILL.md) before starting a new site.

## Reference implementation

[pbcindex.com](https://pbcindex.com): an open index of U.S. mission-locked companies, built to this standard.

## License

[MIT](./LICENSE). Reuse and adapt freely.
