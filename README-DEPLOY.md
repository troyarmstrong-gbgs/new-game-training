# Deploying the Mystery Menu Training page to GitHub Pages

This `github-deploy` folder is self-contained: `index.html`, the two PDFs, the logo,
and the `thumbnails` folder. The **videos are NOT in here** — they're too big for GitHub
(100 MB per-file limit), so they play from YouTube (unlisted). Unlike Google Drive,
YouTube streams inline reliably instead of forcing a download.

Do these two things in order: **(A) put the videos on YouTube and paste the links**, then
**(B) push the folder to GitHub and turn on Pages.**

---

## A. Host the videos on YouTube

1. Upload all 7 videos to YouTube (one channel is fine):
   Rules Video, Full Playthrough, Intro, Feeling Lucky, Feeling Silly, Feeling Smart,
   Feeling Hungry.
2. For **each** video, set **Visibility = Unlisted** (only people with the link can find
   it; it won't show up in search). Public also works. **Private will NOT embed.**
3. On each video, click **Share** → **Copy link**. You'll get something like:
   `https://youtu.be/dQw4w9WgXcQ`
4. Open `index.html` in a text editor and find the `VIDEO_SOURCES` block near the top of
   the `<script>`. Paste each link between the quotes:

   ```javascript
   const VIDEO_SOURCES = {
     "rules":       "https://youtu.be/VIDEOID",
     "playthrough": "https://youtu.be/VIDEOID",
     "intro":       "https://youtu.be/VIDEOID",
     "lucky":       "https://youtu.be/VIDEOID",
     "silly":       "https://youtu.be/VIDEOID",
     "smart":       "https://youtu.be/VIDEOID",
     "hungry":      "https://youtu.be/VIDEOID"
   };
   ```

   (Any YouTube link form works — watch?v=, youtu.be/, or /embed/ — the code pulls the
   ID out automatically. You can also paste just the 11-character ID.)
5. Save the file.

> Tip: open `index.html` by double-clicking it and click each video to confirm it plays
> before you deploy. Videos autoplay when opened.

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
