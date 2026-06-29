# My Portfolio — Local Editor Guide

> Plain HTML · No frameworks · No build step · Edit in any text editor

---

## File Structure

```
portfolio/
├── index.html               ← MAIN PAGE (intro, project cards, article list)
├── assets/
│   ├── css/style.css        ← ALL styles live here (colors, fonts, layout)
│   └── js/main.js           ← Tiny script, usually don't need to touch
├── projects/
│   └── project-template.html  ← COPY this for each new project
├── articles/
│   └── article-template.html  ← COPY this for each new article
├── .github/
│   └── workflows/deploy.yml   ← Auto-deploys to GitHub Pages on push
└── README.md                  ← This file
```

---

## 1 · One-Time Setup (GitHub Pages hosting)

### Step 1 — Create the repo
1. Go to [github.com/new](https://github.com/new)
2. Name it exactly: `yourusername.github.io`  
   *(replace `yourusername` with your actual GitHub username)*
3. Set it to **Public**
4. Click **Create repository**

### Step 2 — Push this folder
```bash
cd portfolio/           # this folder
git init
git add .
git commit -m "initial portfolio"
git branch -M main
git remote add origin https://github.com/yourusername/yourusername.github.io.git
git push -u origin main
```

### Step 3 — Enable GitHub Pages
1. Go to your repo on GitHub → **Settings** → **Pages**
2. Under "Source", select **GitHub Actions**
3. Save.

Your site will be live at `https://yourusername.github.io` within ~60 seconds.

---

## 2 · Preview Locally (Before Pushing)

Open `index.html` directly in your browser for basic preview.

For proper local server (avoids some path issues):

```bash
# Python (usually already installed on Linux/Mac)
cd portfolio/
python3 -m http.server 8080
# → open http://localhost:8080 in browser
```

---

## 3 · Day-to-Day Workflow

```
edit file → save → refresh browser (local preview) → git push (goes live)
```

That's it. No build step, no npm, no anything.

---

## 4 · Common Tasks

### ✏ Update your intro / bio
Open `index.html` — find the `<header id="about">` section.
Edit the `<p class="hero-sub">` paragraph and the `<span>` tags in `.hero-tags`.

---

### 🗂 Add a new project
1. Copy the template:
   ```bash
   cp projects/project-template.html projects/my-new-project.html
   ```
2. Open `projects/my-new-project.html` and fill it in:
   - Change the `<title>` tag
   - Edit `.hero-meta` (category · year)
   - Write your content in the `<article class="prose">` section
   - Add images to `assets/images/` and update the `<img>` `src` paths

3. Add a card on the homepage — open `index.html`, find the `.card-grid` section,
   copy one `<article class="card">` block and update the link, title, description, and tags.

---

### 📝 Add a new article
1. Copy the template:
   ```bash
   cp articles/article-template.html articles/my-new-article.html
   ```
2. Open the new file and write your article.
3. Add a row on the homepage — find `.article-list` in `index.html`,
   copy one `.article-row` block and update the date, title, excerpt, and link.

---

### 🖼 Add images to a page
1. Drop the image file into `assets/images/`
2. Reference it in your HTML:
   ```html
   <img src="../assets/images/your-photo.jpg" alt="description of photo" />
   <p class="img-caption">Your caption here</p>
   ```
   *(for files inside `projects/` or `articles/`, the path starts with `../`)*
   *(from `index.html` at root, use `assets/images/your-photo.jpg`)*

---

### 🎬 Embed a YouTube video
Paste this block anywhere inside `<article class="prose">`:
```html
<div class="video-wrap">
  <iframe src="https://www.youtube.com/embed/VIDEO_ID_HERE" 
    frameborder="0" allowfullscreen></iframe>
</div>
```
Get the `VIDEO_ID` from the YouTube URL: `youtube.com/watch?v=VIDEO_ID_HERE`

---

### 💻 Add a code block
Wrap code in `<pre><code>` tags:
```html
<pre><code>void main(void) {
    HAL_Init();
    /* your code */
}</code></pre>
```

---

### ∑ Add math / equations
Use the `.math-block` div for displayed equations:
```html
<div class="math-block">
  H(s) = Kp + Ki/s + Kd·s
</div>
```

For proper LaTeX rendering, uncomment the MathJax script tag in the page `<head>`:
```html
<script src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-mml-chtml.js"></script>
```
Then write inline math as `\( equation \)` and block math as `\[ equation \]`.

---

### 🎨 Change the accent color
Open `assets/css/style.css` — change the two lines at the top:
```css
--accent:    #4A6741;    ← main color (currently muted green)
--accent-lt: #EDF2EC;    ← light tint used for tag backgrounds
```
Everything updates everywhere automatically.

---

### 🔤 Change your name / initials in the nav
Open every HTML file and find `YN_` — replace with your initials.
Or in `index.html`, find:
```html
<span class="nav-name">YN<span class="cursor">_</span></span>
```

---

## 5 · Push Changes Live

```bash
git add .
git commit -m "add: article on PID controllers"
git push
```

GitHub Actions picks it up automatically. Live in ~60 seconds.
Check progress at: `github.com/yourusername/yourusername.github.io/actions`

---

## 6 · Useful Git Commands

```bash
git status              # see what files changed
git add filename.html   # stage a specific file
git add .               # stage everything
git commit -m "message" # commit with a description
git push                # push to GitHub (goes live)
git log --oneline       # see commit history
git diff                # see what changed before staging
```

---

## 7 · Quick Cheatsheet

| Want to...             | File to edit                        |
|------------------------|-------------------------------------|
| Change bio / intro     | `index.html` → `<header id="about">` |
| Add a project card     | `index.html` → `.card-grid`         |
| Add an article row     | `index.html` → `.article-list`      |
| Write a full project   | copy `projects/project-template.html` |
| Write a full article   | copy `articles/article-template.html` |
| Change colors          | `assets/css/style.css` → `:root {}` |
| Change fonts           | `assets/css/style.css` → `:root {}`  |

---

*No node. No npm. No webpack. Just files.*
