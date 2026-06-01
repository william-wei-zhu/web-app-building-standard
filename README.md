# William's Web App Building Standard

A reusable standard for building small, polished public web apps, so the same design and build decisions don't have to be re-made (or re-requested) on every new project.

It is opinionated by design. The guiding rule is **simplify**: large, high-contrast type; a clean logo + tagline; only the pages that earn their place; and a fixed, boring-on-purpose stack. Projects start from a **pain point**, then a core identity (domain, name, logo, tagline, mission), and everything else is built on top of that.

The full standard lives in **[`SKILL.md`](./SKILL.md)**.

## What it covers

- **Workflow**: start from the core (pain point, domain, name, logo, tagline, mission), then build outward
- **Simplicity first**: remove before you add
- **Typography**: large and legible (~120% base), fonts as principles not fixed faces
- **Color & contrast**: all black or all white, no gray text
- **Theme**: light + dark, system default
- **Brand**: logo and tagline, everywhere they belong
- **Layout**: pagination, non-sticky header, mobile layout optimization (verified at 375 to 390px: responsive headings, no `&nbsp;` clipping, flourishes gated to `sm+`, rows stacked)
- **Required pages**: privacy/disclaimer, about, "Built by William Zhu" footer
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
