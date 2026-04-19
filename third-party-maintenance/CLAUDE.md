# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What This Repo Is

Static HTML pages for Dataknox's Third-Party Maintenance (TPM) service section at `https://www.dataknox.io/third-party-maintenance/`. No build system, no framework, no dependencies — each page is a self-contained `.html` file.

## Site Structure

```
index.html                          ← TPM hub (all categories)
server-maintenance/index.html       ← Server category hub → links to OEM brand pages
storage-maintenance/index.html      ← Storage category hub
network-maintenance/index.html      ← Network category hub
end-of-life-hardware-support/index.html ← EoL support hub
```

OEM brand detail pages (e.g. `server-maintenance/dell-poweredge/index.html`) are created as needed and linked from the category hub.

## Page Architecture

Every page follows the same structure, in order:
1. `<head>` — meta tags, OG tags, Google Fonts (`Barlow Condensed` + `Barlow`), inline `<style>`, JSON-LD schema markup
2. **Nav** — sticky, dark navy, logo SVG inline, links, "Get a Quote" CTA → `mailto:sales@dataknox.io`
3. **Breadcrumb** — `Home › Third-Party Maintenance › [Category]`
4. **Hero** — dark navy, large display heading with `.accent` span in cyan, sub-copy, two CTA buttons
5. **Proof bar** — 5 key stats in dark navy band
6. **Content sections** — alternating `section-white` / `section-alt` / `section-dark`
7. **FAQ** — accordion (toggle `.open` class via inline JS)
8. **CTA band** — full-width cyan background
9. **Footer** — logo, 3-column link groups, cert badges

## Design System (CSS Custom Properties)

All pages share the same `:root` variables (copy exactly):

```css
--dk-navy:#0B1A4A; --dk-navy-mid:#0D2167; --dk-navy-light:#162B7A;
--dk-cyan:#00D4C8; --dk-cyan-bright:#2DEDE6;
--dk-white:#FFFFFF; --dk-white-70:rgba(255,255,255,0.70); --dk-white-40:rgba(255,255,255,0.40);
--dk-teal:#007B7F; --dk-gray-cool:#8B9EC7; --dk-dot-pattern:rgba(0,212,200,0.12);
--dk-font-display:'Barlow Condensed','Impact',sans-serif;
--dk-font-body:'Barlow','DM Sans',sans-serif;
--lt-bg:#FFFFFF; --lt-bg-alt:#F4F6FB; --lt-text:#0B1A4A;
--lt-text-muted:#4A5A7A; --lt-border:rgba(11,26,74,0.10); --lt-cyan-accent:#007B7F;
```

## Key Patterns

- **Styles are inline** in each `<style>` block — no external CSS files. Copy the full style block from an existing page when creating a new one.
- **No JavaScript frameworks** — only a small inline `<script>` for the FAQ accordion at the bottom of `<body>`.
- **All CTAs** link to `mailto:sales@dataknox.io` (quote requests) or `tel:8333282362`.
- **Schema markup** — each page includes `Service` and `FAQPage` JSON-LD in `<head>`. Update `name`, `description`, `url`, and FAQ entries for each new page.
- **OEM brand cards** use `.oem-card` with a `::before` cyan top-border, an `.oem-tag` badge, and a `.card-link` arrow link.
- **URLs** follow the pattern `/third-party-maintenance/[category]/[brand-slug]` (no trailing slash convention inconsistency — check existing pages).

## Creating a New Page

1. Copy the closest existing page (same hierarchy level).
2. Update: `<title>`, `<meta name="description">`, OG tags, breadcrumb `.current`, hero content, proof bar stats, all body sections, FAQ entries, JSON-LD schema.
3. The nav and footer SVG logo, link structure, and cert badges are identical across all pages — do not alter them.
4. Verify internal links in the breadcrumb and "All TPM Services" button are correct for the page's depth.
