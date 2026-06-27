# My Notes Site

A static notes site styled like SQE1 SmartBlocks, with a Decap CMS admin panel.
You log in via GitHub, write notes in a friendly editor, and Netlify rebuilds the site automatically.

## Stack
- **Eleventy** — static site generator (no server needed)
- **Decap CMS** — browser-based admin at `/admin`
- **Netlify** — free hosting + Git Gateway authentication

## Local development

```bash
npm install
npm start          # http://localhost:8080
```

## Deployment (one-time setup)

### 1. Push this folder to a new GitHub repo

```bash
git init
git add .
git commit -m "Initial commit"
git branch -M main
git remote add origin git@github.com:YOUR_USERNAME/my-notes-site.git
git push -u origin main
```

### 2. Connect the repo to Netlify
- Log in to https://app.netlify.com → **Add new site → Import an existing project**
- Pick your GitHub repo. Netlify auto-detects the build settings from `netlify.toml`
- Click **Deploy**

### 3. Enable Decap CMS auth (so only you can edit)
- In Netlify dashboard → **Site configuration → Identity → Enable Identity**
- Under **Registration**, set to **Invite only**
- Under **External providers**, enable **GitHub**
- Scroll to **Services → Git Gateway → Enable**
- Click **Invite users**, send yourself an invite (you'll get an email)
- Click the email link → set a password → you're in

### 4. Update `admin/config.yml`
Change `site_url` and `display_url` to your live Netlify URL.

### 5. Publish notes
- Visit `https://your-site.netlify.app/admin/`
- Log in with the credentials you just set
- Click **New Notes → fill form → Publish**
- Decap commits a `.md` file to GitHub, Netlify rebuilds, note appears live ✨

## Adding a note manually
Create a markdown file in `src/notes/` with frontmatter:

```markdown
---
title: My Note Title
subject: Contract
priority: high
date: 2026-06-27
tags: [offer, acceptance]
---

Note body in **markdown**.
```

## Project structure

```
.
├── admin/                  # Decap CMS panel (static)
│   ├── index.html
│   └── config.yml
├── src/
│   ├── _includes/          # Eleventy layouts
│   │   ├── base.njk
│   │   └── note.njk
│   ├── css/style.css       # SmartBlocks design system
│   ├── notes/              # Your markdown notes live here
│   │   ├── notes.json      # Directory data (layout + permalink)
│   │   └── *.md
│   └── index.njk           # Homepage (lists notes by subject)
├── .eleventy.js            # Eleventy config
├── netlify.toml            # Netlify build config
└── package.json
```

## Customisation

- **Subjects list**: edit the `options` array in `admin/config.yml`
- **Colours/fonts**: edit `src/css/style.css`
- **Brand name**: edit `src/_includes/base.njk` (search for `MyNotes`)
