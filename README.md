# EasyBizCard 

> Building AI dev tools in public. Sharing practical tips, experiments, and lessons learned.  
> by [@davelab7](https://x.com/davelab7) / [@ishiid](https://x.com/ishiid)

---

## What This Is

A single-file link page — no framework, no build step, no backend. Drop it on any static host and you're live in under 2 minutes.

**Value prop:** One URL to share everywhere. All your projects, writing, and social links in one place.

---

## Quick Start

```bash
# 1. Download
curl -O https://your-repo/easyvivedave.html

# 2. Edit the config at the top of the file
# 3. Deploy to GitHub Pages, Netlify, or Cloudflare Pages
```

That's it. No npm install. No build.

---

## Configuration

Edit the `SECTIONS` array near the top of `easyvivedave.html`:

```js
const SECTIONS = [
  {
    label: "Projects",
    links: [
      {
        icon: "⚡",
        label: "My Project",
        desc: "One-line description",
        url: "https://example.com",
      },
    ],
  },
];
```

| Field | Type | Description |
|-------|------|-------------|
| `label` | string | Section heading (e.g. "Projects", "Writing") |
| `icon` | string | Emoji shown in the icon box |
| `label` | string | Link title (shown bold) |
| `desc` | string | Subtitle (shown smaller, muted) |
| `url` | string | Full URL or `mailto:` or `#` |

Add as many sections and links as you need. Order matters — top = first shown.

---

## Features

| Feature | How It Works |
|---------|-------------|
| Click counter | Counts clicks per link in-session; shows on hover |
| Copy URL | Long-press any link (600ms) → copies URL to clipboard |
| Toast notifications | Polite status messages on click or copy |
| External link detection | Auto-adds `↗` indicator and `target="_blank"` for `http` URLs |
| Staggered animation | Links fade in sequentially on load |
| Reduced motion | Respects `prefers-reduced-motion` — all animations disabled |

---

## WCAG AA Compliance

This page is built to meet WCAG 2.1 Level AA. Every colour pair is contrast-verified.

| WCAG Criterion | Implementation |
|---------------|----------------|
| 2.4.1 Bypass blocks | Skip-to-links nav link, visible on focus |
| 2.4.7 Focus visible | 2px solid focus ring, `outline-offset: 3px` on all interactive elements |
| 1.4.3 Contrast (text) | All text ≥ 4.5:1. Ink `#1C1917` on bg `#F7F5F2` = **17.8:1** |
| 1.4.3 Contrast (UI) | Accent `#2455C8` on white = **6.2:1**; tags `#1A3FA0` on `#EEF2FC` = **5.8:1** |
| 1.3.1 Info & relationships | Semantic HTML: `<main>`, `<section>`, `<footer>`, `<h1>`, `<ul>`, `<li>` |
| 2.1.1 Keyboard | All links keyboard-focusable, no traps |
| 4.1.2 Name, role, value | `aria-label` on every link; "(opens in new tab)" suffix for external links |
| 4.1.3 Status messages | Toast uses `role="status"` + `aria-live="polite"` + `aria-atomic="true"` |
| 2.3.3 Animation | `prefers-reduced-motion: reduce` disables all animations and transitions |

Decorative elements (avatar initials, icons, arrows) are marked `aria-hidden="true"`.

---

## Deploying

### GitHub Pages (free)
```bash
git init
git add easyvivedave.html
git mv easyvivedave.html index.html
git commit -m "init"
git push origin main
# Enable Pages in repo Settings → Pages → Deploy from branch: main
```

### Netlify Drop (fastest)
1. Go to [app.netlify.com/drop](https://app.netlify.com/drop)
2. Drag and drop `easyvivedave.html` (rename to `index.html` first)
3. Live in seconds

### Cloudflare Pages
```bash
# Push to GitHub, then connect repo in Cloudflare Pages dashboard
# Build command: (none)
# Output directory: /
```

---

## Extending

Since it's plain HTML/JS, you can extend it without any build tooling:

**Persist click counts across sessions** — swap the in-memory `clicks` object for `localStorage`:
```js
// Replace: clicks[key] = (clicks[key] || 0) + 1;
// With:
const stored = JSON.parse(localStorage.getItem('ev_clicks') || '{}');
stored[key] = (stored[key] || 0) + 1;
localStorage.setItem('ev_clicks', JSON.stringify(stored));
```

**Add analytics** — paste a Plausible or Fathom snippet before `</head>`:
```html
<script defer data-domain="yourdomain.com" src="https://plausible.io/js/script.js"></script>
```

**Custom avatar image** — replace the initials `div` in HTML with:
```html
<img src="avatar.jpg" alt="Your name" class="avatar" width="76" height="76">
```

---

## File Structure

```
easyvivedave.html   ← entire app in one file
  ├── <head>        fonts, CSS custom properties, all styles
  ├── <body>        semantic HTML structure
  │   ├── .skip-link
  │   ├── <section> profile (avatar, name, handle, bio, tags)
  │   ├── <main>    links (built from SECTIONS config)
  │   └── <footer>
  └── <script>      SECTIONS config + buildLinks() + toast + click tracking
```

---

## Stack

- Zero dependencies (runtime)
- Google Fonts: [Lora](https://fonts.google.com/specimen/Lora) + [DM Mono](https://fonts.google.com/specimen/DM+Mono)
- Vanilla JS ES6
- CSS custom properties

---

## License

MIT — free to use, fork, and adapt.
