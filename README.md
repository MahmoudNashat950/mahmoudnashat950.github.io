# Mahmoud Nashaat — Portfolio

A static, single-page freelance portfolio for an AI & Data Engineer. Pure HTML, CSS, and vanilla JavaScript — no build step, no backend, no paid services. Built to deploy for free on GitHub Pages.

## Folder structure

```text
.
├── index.html          Main page (all sections)
├── 404.html            Custom "page not found" page
├── .nojekyll           Tells GitHub Pages to skip Jekyll processing
├── css/
│   └── styles.css      All styles (design tokens at the top)
├── js/
│   └── main.js         Mobile nav, scroll-reveal, active nav link, footer year
├── assets/
│   └── favicon.svg     Site icon
└── README.md           This file
```

## Preview locally

You don't need Node or any build tool. From this folder, run any static server, for example:

```bash
python3 -m http.server 8000
```

Then open `http://localhost:8000` in your browser.

Opening `index.html` directly by double-clicking also works, but a local server is closer to how GitHub Pages will actually serve it.

---

## Deploying to GitHub Pages (free)

You want the site available at `https://mahmoudnashat950.github.io/` — the **root** of your GitHub Pages domain, with no `/repo-name/` in the URL. That specific URL format requires a **user site**, which GitHub Pages only creates from a repository with one exact name.

### 1. Create the repository with the exact right name

Create a new **public** GitHub repository named exactly:

```text
mahmoudnashat950.github.io
```

(All lowercase, matching your GitHub username exactly, including `.github.io` at the end.) This exact naming is what tells GitHub to treat it as your user site and serve it at the root domain instead of a `/repo-name/` sub-path.

### 2. Push this code to the repository

From this folder:

```bash
git init
git add .
git commit -m "Initial portfolio site"
git branch -M main
git remote add origin https://github.com/MahmoudNashat950/mahmoudnashat950.github.io.git
git push -u origin main
```

### 3. Turn on GitHub Pages

1. Go to the repository on GitHub → **Settings** → **Pages**.
2. Under **Build and deployment** → **Source**, choose **Deploy from a branch**.
3. Under **Branch**, choose `main` and folder `/ (root)`, then **Save**.
4. Wait 1–2 minutes. Your site will go live at:

```text
https://mahmoudnashat950.github.io/
```

Every time you push new commits to `main`, GitHub Pages redeploys automatically — no extra steps needed.

> **Note on the repository name:** if you'd rather keep this project under a different (project-style) repo name, GitHub Pages will instead serve it at `https://mahmoudnashat950.github.io/that-repo-name/`. All the links in this site use relative paths (`css/styles.css`, `js/main.js`, `#section-ids`), so it will still work correctly at a sub-path — it just won't match the exact root URL you specified. Use the `mahmoudnashat950.github.io` repo name if the root URL matters to you.

---

## Before you publish: things to fill in

This site intentionally ships with **placeholders** instead of invented contact details. Search for these two placeholder strings and replace every occurrence:

| Placeholder | Replace with | Found in |
| --- | --- | --- |
| `YOUR_EMAIL@example.com` | Your real email address | `index.html` (contact section, footer) |
| `YOUR-LINKEDIN-USERNAME` | Your real LinkedIn username/slug | `index.html` (contact section, footer) |

Quick way to find them all:

```bash
grep -rn "YOUR_EMAIL\|YOUR-LINKEDIN-USERNAME" index.html
```

Each appears twice (once in the Contact section, once in the footer) — four lines total.

---

## Adding a new project later

Projects live in two places in `index.html`:

1. **A card in the "Featured projects" grid** (`<section id="projects">`). Copy one of the existing `<article class="project-card">` blocks, and update the title, description, `tech-badge` list, and GitHub link(s).
2. **(Optional) A full case study** (`<section id="case-studies">`) if the project deserves the longer Problem → Solution → Architecture → Technologies → Highlights → Results → GitHub treatment. Copy an existing `<article class="case-study">` block as a starting point. Link to it from the project card with `<a href="#your-new-case-study-id">Read case study</a>`.

If you add a new architecture diagram, reuse the existing patterns in `styles.css`:

- `.arch-diagram` / `.arch-node` / `.arch-branch` — for a router-style flow with a branch (like the Retail Analytics Copilot).
- `.arch-pipeline` — for a straight left-to-right pipeline (like the medallion Bronze/Silver/Gold flow). It automatically stacks vertically on mobile.

---

## Connecting a custom domain later (optional)

If you later buy a domain (e.g. `mahmoudnashaat.com`):

1. At your domain registrar, add either:
   - An **A record** pointing `@` to GitHub's Pages IPs: `185.199.108.153`, `185.199.109.153`, `185.199.110.153`, `185.199.111.153`, or
   - A **CNAME record** pointing a subdomain (e.g. `www`) to `mahmoudnashat950.github.io`.
2. In the repository, go to **Settings → Pages → Custom domain**, enter your domain, and save. GitHub will create a `CNAME` file in your repo automatically.
3. Wait for DNS to propagate (can take up to a few hours), then enable **Enforce HTTPS** in the same settings panel once it becomes available.

You don't need to do anything else in the code — all links here are relative, so the site works the same on any domain.

---

## Customizing colors and fonts

Everything visual is controlled by CSS custom properties at the top of `css/styles.css`, under `:root`. For example:

```css
--gold:  #B8842A;   /* primary accent */
--teal:  #1F6F5C;   /* secondary accent */
--paper: #F3F4F1;   /* page background */
--ink:   #15181C;   /* text / dark panels */
```

Change these values and the whole site updates consistently — buttons, badges, links, diagram accents, etc.

Fonts are loaded from Google Fonts in the `<head>` of `index.html` and `404.html` (IBM Plex Mono for headings/labels, IBM Plex Sans for body text). Swap the `<link>` tag and the `--font-display` / `--font-body` variables in `styles.css` to change them.

---

## Notes

- **No frameworks, no build step.** Just HTML/CSS/JS, so there's nothing to install or compile.
- **No backend, database, or paid API.** The contact section links to `mailto:` and external profiles only.
- **Accessibility:** semantic HTML, visible focus states, alt text where images exist, and `prefers-reduced-motion` is respected throughout. Content is fully visible even with JavaScript disabled (progressive enhancement — the JS only adds animation, never hides content permanently).
- **Performance:** two font families, no images beyond a tiny SVG favicon, no external JS libraries.
