# Staff Backend Engineer - 8-Week Prep Tracker

A single-file, interactive study tracker for an 8-week Staff / Staff Backend
Engineer preparation plan. Built to be hosted on **GitHub Pages** with zero
build step - it is just static HTML + a bit of JavaScript.

**Time split (10 hrs/week):** 6h System Design - 2.5h DSA - 1.5h Staff skills.

## Live site

Once GitHub Pages is enabled (see below), it will be at:


Because the app file is named `index.html`, it loads automatically at the site
root - no extra path needed.

## Features

- Checkbox for every task across all 8 weeks, grouped into 3 tracks.
- Per-track progress bars + overall completion bar + per-week percentage.
- Time-allocation donut chart (Chart.js).
- Collapsible "+ sources" under each task: curated links + video items
  (shown as channel + exact title, so a search always finds them).
- Collapse / expand all weeks.
- Export / Import progress as JSON (see below).
- Reset all progress.

## How your progress is stored (read this)

Progress lives in your browser's **localStorage** - nothing is uploaded, there
is no backend. Two consequences:

- Progress is **per-browser and per-device**. Your laptop and your phone keep
  separate progress. Different browsers do too.
- To move or back up progress, use **Export progress** (downloads a JSON file)
  and **Import progress** (loads one back in). This is the only way to sync
  across devices or survive clearing browser data.

The Import accepts either the exported wrapper file or a raw state object.

## Enable GitHub Pages

1. Create a repo on GitHub and push these files (`index.html`, `README.md`,
   `.gitignore`, and `8-week-plan.md` if you want the written plan too).
2. In the repo: **Settings -> Pages**.
3. Under **Build and deployment -> Source**, choose **Deploy from a branch**.
4. Branch: `main` (or `master`), folder: `/ (root)`. Save.
5. Wait ~1 minute, then open the URL shown on that Pages settings screen.

### Push commands (run these yourself)

```bash
cd /Users/s0r0g3z/staff-eng-prep
git init
git add index.html README.md .gitignore 8-week-plan.md
git commit -m "Add Staff Engineer 8-week prep tracker"
git branch -M main
git remote add origin https://github.com/<your-username>/<repo-name>.git
git push -u origin main
```

## Privacy note

If the repo is **public**, the page is publicly viewable by anyone with the URL.
It contains only a study plan (no secrets, no personal data), so that is fine.
Use a private repo if you prefer - note GitHub Pages on private repos requires a
paid plan to keep the published site private.

## Files

- `index.html` - the tracker app (self-contained).
- `8-week-plan.md` - the full written curriculum.
- `README.md` - this file.
- `.gitignore` - ignores OS/editor cruft.
