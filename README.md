# Mehwish — Portfolio (Vector Art Edition): Build & Deploy Guide

A single-page portfolio built with **plain HTML, CSS and JavaScript**. There is no framework, no build step and no installs, so anyone can open, edit and host it for free.

## 1. What it is made of

| Piece | What it does |
|---|---|
| **HTML** | The structure: header, hero, projects, writing, services, background, contact |
| **CSS** | Layout with Grid and Flexbox, colour variables for light and dark mode, `color-mix()` tints, media queries for responsive design |
| **JavaScript (vanilla)** | Theme toggle, scroll-reveal, interactive dashboard, email chooser, mouse tilt |
| **Inline SVG** | The flat vector illustrations (magnifier, plant, shapes, coffee), icons and wave dividers, plus the dashboard charts (drawn by JS) |
| **Google Fonts** | Inter (body), Outfit (headings), Fraunces (small accents) |
| **Git + GitHub** | Stores your code |
| **Vercel (or similar)** | Hosts it live for free |

## 2. Folder structure

```
portfolio/
├── index.html     <- the whole site (HTML + CSS + JS)
└── README.md      <- this guide
```

## 3. Step by step

### Step 1: Install the tools
1. Install **VS Code**: https://code.visualstudio.com
2. Install **Git**: https://git-scm.com/downloads
3. Make a free **GitHub** account (you already have one: Mehwish4610)
4. In VS Code, install the extension **Live Server** (by Ritwick Dey)

### Step 2: Create the project
1. Make a folder called `portfolio` on your computer.
2. Put `index.html` inside it.
3. Open the folder in VS Code (File > Open Folder).

### Step 3: Run it on your computer
- Right-click `index.html` > **Open with Live Server**, or just double-click the file.
- The page opens in your browser and reloads whenever you save.

### Step 4: Understand the code (open `index.html`)
Search (Ctrl+F) for these names to find each part:

**In `<head>`**
- `<link href="https://fonts.googleapis.com...` loads the fonts.
- `<meta name="description"...` is what Google shows under your link.
- `<style>`: all the CSS. It is built in layers, so the **last block, `/* ---- vector art layer ---- */`, decides the final look**.

**Colours (edit these)**: in the vector layer's `:root{...}`
- `--bg` page background, `--fg` text, `--acc` link/accent colour
- `--v1 --v2 --v3 --v4` the four illustration colours (coral, yellow, teal, indigo)
- A second set under `prefers-color-scheme:dark` and `[data-theme="dark"]` gives dark mode.

**In `<body>` (search these ids)**
- `class="hero"`: headline, intro, stats (5+, 2+, 1)
- `class="stage"`: the dashboard with the floating SVG illustrations (`.dc .s1` to `.s4`)
- `id="work"`: projects (each is a `<div class="row rv">`)
- `id="writing"`: Medium article card
- `id="services"`: three service cards + 3 process steps
- `id="about"`: timeline, experience, certificates, publication
- `id="contact"`: contact buttons
- `id="mm"`: the email chooser pop-up (Gmail / Outlook / Yahoo / default / copy)

**In the `<script>` at the bottom**
- Theme toggle: saves your choice in `localStorage`.
- Scroll reveal: `IntersectionObserver` fades sections in.
- Dashboard data: arrays `YR`, `TK` (tickets per year), `CT` (categories) and `BR` (bars). **Change these numbers to change the charts.**
- Chart functions: `kp()` KPIs, `ln()` line chart, `dn()` donut, `br()` bars. They build SVG as text.
- Filter chips and Tickets / YoY growth / Cumulative buttons update the charts.
- Mouse tilt on the dashboard window, and the email pop-up open/close logic.

### Step 5: Customise it
- **Text:** edit the words between the tags.
- **Add a project:** copy one `<div class="row rv">...</div>` block, change the number, title, description, tags and links.
- **Links:** search for `https://github.com/Mehwish4610` and replace with exact repo links if needed.
- **Email:** search `mehwishafreen10303` (appears in the contact button and the email pop-up).
- **Colours:** change the `--v1` to `--v4` values.

### Step 6: Put it on GitHub
In the project folder, open a terminal (in VS Code: Terminal > New Terminal):

```bash
git init
git add .
git commit -m "Initial portfolio"
git branch -M main
git remote add origin https://github.com/Mehwish4610/portfolio.git
git push -u origin main
```
(Create an empty repo named `portfolio` on github.com first: New repository, no README.)

### Step 7: Deploy it free

**Option A: Vercel (easiest, auto-updates)**
1. Go to https://vercel.com and **Sign up with GitHub**.
2. Click **Add New > Project**, then **Import** your `portfolio` repo.
3. Framework Preset: **Other**. Leave Build Command and Output Directory empty.
4. Click **Deploy**. In about a minute you get a live link like `portfolio-xxxx.vercel.app`.
5. From now on, every `git push` updates the live site automatically.

**Option B: GitHub Pages (no extra account)**
1. Repo > **Settings > Pages**.
2. Source: **Deploy from a branch**, branch **main**, folder **/ (root)**, Save.
3. Live at `https://mehwish4610.github.io/portfolio/` (name the repo `Mehwish4610.github.io` to get `https://mehwish4610.github.io/`).

**Option C: Netlify Drop (no Git needed)**
Go to https://app.netlify.com/drop and drag your `portfolio` folder onto the page.

**Option D: Cloudflare Pages**
Connect your GitHub repo at https://pages.cloudflare.com, with no build command.

All four have free plans. Free-plan terms and limits change, so check each site's current pricing page. If you plan to host paid client work, read the plan's terms (some free plans are for personal use only).

### Step 8: Optional upgrades
- **Custom domain** (e.g. mehwish.dev): buy one from any registrar, then add it in Vercel > Project > Settings > Domains and follow the DNS steps.
- **Share link preview:** add an `og:image` meta tag with a 1200x630 screenshot of your site.
- **Visitor stats:** free tools like Vercel Analytics or Cloudflare Web Analytics.

## 4. Before you share the link (checklist)
- [ ] Click every button: project links, certificates, paper, Medium, LinkedIn, GitHub, X
- [ ] Test the email pop-up (Gmail, Outlook, default app, copy)
- [ ] Check light and dark mode (the ◐ button)
- [ ] Check on your phone and another screen size (in Chrome: F12, then Ctrl+Shift+M to simulate devices)
- [ ] Check the Google Drive certificate links open without signing in (sharing: "Anyone with the link")
- [ ] Run Chrome **Lighthouse** (F12 > Lighthouse) for speed and accessibility

## 5. Troubleshooting
| Problem | Fix |
|---|---|
| Fonts look different | You're offline. Fonts load from Google Fonts |
| Live site didn't update | Make sure you ran `git add . && git commit && git push` |
| Vercel shows 404 | Make sure the file is named exactly `index.html`, at the top level of the repo |
| Charts don't draw | Open DevTools (F12) > Console for the error line |
| Changes to colours don't show | Edit the **last** `:root{...}` block (the vector layer), because it overrides earlier ones |
