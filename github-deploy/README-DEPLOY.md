# Deploying the Mystery Menu Training page to GitHub Pages

This `github-deploy` folder is self-contained: `index.html`, the two PDFs, the logo,
and the `thumbnails` folder. The **videos are NOT in here** — they're too big for GitHub
(100 MB per-file limit), so they stream from Google Drive.

Do these two things in order: **(A) put the videos on Drive and paste the links**, then
**(B) push the folder to GitHub and turn on Pages.**

---

## A. Host the videos on Google Drive

1. Upload all 6 videos to a folder in Google Drive:
   Rules Video, Intro, Feeling Lucky, Feeling Silly, Feeling Smart, Feeling Hungry.
2. For **each** video: right-click → **Share** → under "General access" choose
   **Anyone with the link** → role **Viewer**. (If they're not shared this way, they
   won't play on the site.)
3. Right-click each video → **Copy link**. You'll get something like:
   `https://drive.google.com/file/d/1AbCdEfGhIjKlMnOpQr.../view?usp=sharing`
4. Open `index.html` in a text editor and find the `VIDEO_SOURCES` block near the top of
   the `<script>`. Paste each link between the quotes:

   ```javascript
   const VIDEO_SOURCES = {
     "rules":  "https://drive.google.com/file/d/1kPNxweOwK6ws1D_ozV42eXiGph_HJ44C/view?usp=drive_link",
     "intro":  "https://drive.google.com/file/d/1N5V865o-7J6AmqUowZLIPhNd-bwRI84s/view?usp=drive_link",
     "lucky":  "https://drive.google.com/file/d/1z44q7MVy4i4iFKwX8rFzR9_E5DnkApya/view?usp=drive_link",
     "silly":  "https://drive.google.com/file/d/17w3DVi777a6_3uINBnfmKyxHEV0rntVS/view?usp=drive_link",
     "smart":  "https://drive.google.com/file/d/1Tc4PAehH6-JmaSVsxV-BG4btji9AXmG3/view?usp=drive_link",
     "hungry": "https://drive.google.com/file/d/1dXyLE7VJL9gvZkJ0AnPU4kYee63qJMSg/view?usp=drive_link"
   };
   ```

   (You can paste the full link — the code pulls the file ID out automatically.)
5. Save the file.

> Tip: open `index.html` by double-clicking it and click a video to confirm each one
> plays before you deploy.

---

## B. Publish with GitHub Pages

### Option 1 — GitHub website (no command line)

1. Go to https://github.com and create a **new repository** (e.g. `mystery-menu-training`).
   Public is simplest; Pages also works on private repos with a paid plan.
2. On the new repo page, click **Add file → Upload files**.
3. Drag in the **contents** of this `github-deploy` folder — that's `index.html`, both
   PDFs, `mystery-menu.png`, and the `thumbnails` folder. (Upload the files/folder
   themselves, not the outer `github-deploy` folder.)
4. Click **Commit changes**.
5. Go to **Settings → Pages**.
6. Under "Build and deployment", set **Source: Deploy from a branch**, **Branch: main**,
   folder **/ (root)**, then **Save**.
7. Wait ~1 minute. Your site appears at:
   `https://YOUR-USERNAME.github.io/mystery-menu-training/`

### Option 2 — command line (git)

```bash
cd "github-deploy"
git init
git add .
git commit -m "Mystery Menu training page"
git branch -M main
git remote add origin https://github.com/YOUR-USERNAME/mystery-menu-training.git
git push -u origin main
```

Then do steps 5–7 above (Settings → Pages).

---

## Notes

- **Sign-off still works on the live site.** The button posts to your existing Google
  Apps Script endpoint (already wired in), which writes to your Sheet.
- The sign-off button stays locked until a host opens all 6 videos + 2 PDFs and ticks the
  confirmation box.
- To update anything later, edit the file(s) and re-upload / `git push`; Pages redeploys
  automatically.
- If a video shows "can't be played," it's almost always the Drive sharing setting —
  re-check step A.2.
