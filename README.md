# Hamza Tariq — Engineering Portfolio

A static personal portfolio (HTML, CSS, vanilla JavaScript). No build step, no frameworks, no backend. It is designed to be hosted free on **GitHub Pages**.

## Project structure

```
.
├── index.html                  Home page (hero, about, skills, experience, projects, education, leadership, contact)
├── projects/
│   ├── index.html              All projects (incl. firefighting robot, wind turbine, rope braiding, course projects)
│   ├── autodidact.html         AUTODIDACT case study
│   └── bat-uav.html            Bat-inspired micro UAV case study
├── css/style.css               All styles and design tokens (colours, type, spacing at the top)
├── js/
│   ├── config.js               ← EDIT THIS: GitHub URL, project images, repository links
│   └── main.js                 Navigation, image loading, hero animation
├── assets/
│   ├── Hamza_Tariq_CV.pdf      CV served by every "Download CV" button
│   ├── favicon.svg
│   ├── fonts/                  Self-hosted Archivo + JetBrains Mono (SIL OFL licences included)
│   └── images/                 Put your project images here
├── .github/workflows/deploy.yml  Automatic deployment to GitHub Pages
├── .nojekyll                   Tells GitHub Pages to serve files as-is
└── robots.txt
```

## Preview locally

Any static server works. From this folder:

```bash
python3 -m http.server 8000
# open http://localhost:8000
```

(Opening `index.html` directly also works for most things.)

## 1. Add your GitHub profile

Open `js/config.js` and fill in:

```js
github: "https://github.com/YOUR-USERNAME",
```

While this is empty, all GitHub links stay hidden, so the site never shows a broken link.

## 2. Replace image placeholders

Every placeholder on the site shows a **slot name** (for example `slot: autodidact-mujoco`). To fill one:

1. Copy your image into `assets/images/` (JPG, PNG or WebP; around 1600 px wide is plenty).
2. Register it in `js/config.js`:

```js
images: {
  "autodidact-mujoco": "mujoco-twin.png",
  "uav-prototype": "uav-prototype.jpg",
},
```

Available slots:

| Slot | Where it appears |
|---|---|
| `autodidact-cover` | AUTODIDACT card (home + all projects) |
| `autodidact-environment` | Case study: simulated robot environment |
| `autodidact-mujoco` | Case study: MuJoCo simulation |
| `autodidact-architecture` | Case study: original architecture diagram |
| `autodidact-dashboard` | Case study: system dashboard |
| `autodidact-team` | Case study: hackathon presentation / team photo |
| `uav-cover` | UAV card (home + all projects) |
| `uav-cad` | Case study: CAD model |
| `uav-mechanism` | Case study: wing mechanism |
| `uav-printed-parts` | Case study: 3D-printed components |
| `uav-cfd` | Case study: CFD / FEA results |
| `uav-adams` | Case study: MSC Adams simulation |
| `uav-prototype` | Case study: prototype photo |
| `uav-testing` | Case study: wind-tunnel / field test |
| `firefighting-cover` | Firefighting robot (home card + all projects) |
| `wind-turbine-cover` | Wind turbine (home card + all projects) |
| `rope-braiding-cover` | Rope braiding machine (home card + all projects) |

Each image's alt text is taken from the `data-alt` attribute in the HTML. Edit it there if you want a more specific description.

On the home page, cards without an image show a line illustration labelled "Concept illustration". Adding an image replaces it automatically.

## 3. Update your CV

Replace `assets/Hamza_Tariq_CV.pdf` with the new file **using the same name**. All download buttons update automatically.

## 4. Optional: link project repositories

In `js/config.js`:

```js
repos: { "autodidact": "https://github.com/YOUR-USERNAME/autodidact" }
```

A "View repository" link then appears on the AUTODIDACT case study.

## Deploy to GitHub Pages

### First time

1. On GitHub, create a new **public** repository, e.g. `portfolio`.
   (If you name it `YOUR-USERNAME.github.io`, the site will live at `https://YOUR-USERNAME.github.io/` instead of `/portfolio/`.)
2. Push this folder to it:

   ```bash
   cd path/to/this/folder
   git init
   git add .
   git commit -m "Initial portfolio"
   git branch -M main
   git remote add origin https://github.com/YOUR-USERNAME/portfolio.git
   git push -u origin main
   ```

   No Git on your machine? On the empty repository page choose **uploading an existing file** and drag in the folder contents. Include the hidden `.github` folder and `.nojekyll`. On macOS press Cmd+Shift+. in Finder to show hidden files.
3. In the repository go to **Settings → Pages → Build and deployment → Source** and choose **GitHub Actions**.
4. Open the **Actions** tab. The "Deploy to GitHub Pages" workflow runs and, after about a minute, shows the live URL, e.g. `https://YOUR-USERNAME.github.io/portfolio/`.

### Updating

Edit, commit and push to `main`. The site redeploys automatically.

```bash
git add .
git commit -m "Add UAV photos"
git push
```

### Alternative without Actions

Settings → Pages → Source: **Deploy from a branch** → `main` / `(root)`. This works too, because all paths are relative.

## Before publishing — checklist

- [ ] GitHub URL added in `js/config.js`
- [ ] Real project images added (at least `autodidact-cover` and `uav-cover`)
- [ ] "Lessons learned" (AUTODIDACT) and "Takeaways" (UAV) reviewed. They are marked as drafts in the HTML comments and should be in your own words.
- [ ] Decide whether you want your phone number public. To remove it, delete the "Phone" block in the contact section of `index.html`.
- [ ] Optional: add details to the firefighting robot entry in `projects/index.html` (sensors, controller, results).
- [ ] Optional: after deploying, add `<meta property="og:image" content="https://…/assets/images/social.jpg">` to each page for a link-preview image.

## Customising the design

All colours, fonts and spacing are CSS variables at the top of `css/style.css` (`--brass` is the accent colour, `--steel` is the drawing line colour). The hero drawing is an inline SVG in `index.html`, and its animation is at the bottom of `js/main.js`. It respects the operating system's "reduce motion" setting.
