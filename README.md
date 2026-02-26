# Data Engineering Handbook

A practical guide to building scalable data systems — from fundamentals to production pipelines.

## 🌐 Hosting on GitHub Pages

This site is a **static HTML website** designed to be hosted on GitHub Pages. Follow these steps:

### 1. Create a GitHub repository

1. Go to [github.com/new](https://github.com/new)
2. Name it `DataEnggHandbook` (or `username.github.io` for a personal site)
3. Set visibility to **Public**
4. Create the repository (don't add README if you're pushing this project)

### 2. Push your code

```bash
cd DataEnggHandbook
git init
git add .
git commit -m "Initial commit: Data Engineering Handbook"
git branch -M main
git remote add origin https://github.com/YOUR_USERNAME/DataEnggHandbook.git
git push -u origin main
```

### 3. Enable GitHub Pages

1. Go to your repo → **Settings** → **Pages** (under "Code and automation")
2. Under **Source**, select **Deploy from a branch**
3. Choose branch: **main**, folder: **/ (root)**
4. Click **Save**

### 4. View your site

After a few minutes, your site will be live at:

- **Project site:** `https://YOUR_USERNAME.github.io/DataEnggHandbook/`
- **User site** (if repo is `username.github.io`): `https://YOUR_USERNAME.github.io/`

---

## 📁 Project structure

```
DataEnggHandbook/
├── index.html          # Homepage
├── chapters/           # Chapter content (from data_engg_handbook)
│   ├── chapter1.md     # Linux & Database Fundamentals
│   ├── chapter2.md     # Keys, Scala Basics
│   └── ...            # chapters 3–36
├── fundamentals.html  # Core concepts
├── pipelines.html      # Data pipeline design
├── storage.html        # Storage & databases
├── tools.html          # Tools & technologies
├── styles.css          # Shared styles
├── .nojekyll           # Bypasses Jekyll (required for plain HTML)
└── README.md
```

## ✏️ Adding content

Edit the markdown files in `chapters/` to update chapter content. Add new chapters by creating `chapterN.md` and adding a link in `chapters.html`.
