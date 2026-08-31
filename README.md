# Ariq Ulwan — Portfolio

Plain static site. No build step, no npm install, no dependencies.

---

## Deploy on GitHub Pages

### 1. Create the repo
On GitHub, create a new **public** repo. Two options:

- `Rikue29.github.io` → site lives at `https://rikue29.github.io/`
- any other name, e.g. `portfolio` → site lives at `https://rikue29.github.io/portfolio/`

Don't add a README or .gitignore during creation (keeps it clean).

### 2. Copy the files in
Put **everything in this folder** into the repo root — `index.html` must sit at the top level, not inside a subfolder.

Include the **hidden files**: `.nojekyll` and `.image-slots.state.json`. macOS Finder and some unzip tools hide them. If you're unsure, press `Cmd+Shift+.` in Finder (or enable "show hidden files") to confirm both are there.

`.image-slots.state.json` holds every project screenshot you dropped in. Without it the project cards render empty.

### 3. Push
```bash
cd path/to/this/folder
git init
git add -A
git commit -m "portfolio"
git branch -M main
git remote add origin https://github.com/Rikue29/<repo>.git
git push -u origin main
```

Verify the hidden files made it: `git ls-files | grep image-slots` should print the sidecar. If it doesn't, run `git add -f .image-slots.state.json .nojekyll` and commit again.

### 4. Turn on Pages
Repo → **Settings** → **Pages** → Source: **Deploy from a branch** → Branch: `main`, folder `/ (root)` → **Save**.

Live in about a minute. First build can take up to 5.

---

## Local preview

Must be served over HTTP — opening `index.html` by double-clicking gives a `file://` origin, which blocks the runtime and the images.

```bash
python3 -m http.server 8000
```
Then open http://localhost:8000

---

## What's in here

| File | Purpose |
|---|---|
| `index.html` | The entire site — markup, styles and logic inline |
| `support.js` | Runtime that renders the page |
| `image-slot.js` | Project image slots |
| `.image-slots.state.json` | Your dropped project screenshots |
| `portrait.png` | Hero headshot |
| `avatar-shahrul.png`, `avatar-shane.png` | Recommendation avatars |
| `assets/00017.wav`, `assets/00019.wav` | Open / close UI sounds |
| `.nojekyll` | Stops GitHub Pages from stripping dotfiles |

---

## Editing after deploy

Everything is in `index.html`. Text, colours and links are plain HTML/CSS inside it — edit, commit, push, and Pages redeploys automatically.

To swap a project screenshot: run locally, drag a new image onto the slot, then commit the updated `.image-slots.state.json`.

---

## Custom domain (optional)

1. Add a file named `CNAME` at the repo root containing just your domain, e.g. `ariqulwan.com`
2. At your DNS provider, add a `CNAME` record pointing your domain at `rikue29.github.io`
3. Settings → Pages → Custom domain → enter it → tick **Enforce HTTPS**

---

## Troubleshooting

**Blank page** — `index.html` isn't at the repo root, or `support.js` didn't get committed. Check the browser console (F12).

**Project cards empty** — `.image-slots.state.json` is missing. See step 2.

**No sound** — browsers block audio until you interact with the page. Click anywhere first; it's not a bug.

**404 after enabling Pages** — wait a few minutes, then hard-refresh (`Cmd+Shift+R`). Check Actions tab for a failed deploy.
