# Tee Sheet Builder

A single-file web app for making **cart signs** and a **pairing sheet** for a golf group.
Type in who's playing and which foursome they're in, and it prints ready-to-go signs. No
install, no sign-in, no accounts. It's one HTML file.

- Cart signs (one per group) and a master pairing sheet, both print-ready
- Auto-calculates strokes off the lowest course handicap in each group
- Optional tee time / starting hole per group
- Remembers the roster between visits (when served from a URL — see below)
- Copy/paste backup so the roster can move between devices

---

## Deploy it (GitHub Pages)

Hosting it at a real web address is what makes it nicest to use: it opens in Safari, can be
added to the Home Screen like an app, and the "remembers your roster" feature works.

1. **Rename the app file to `index.html`** and put it in the repo root.
   (GitHub Pages serves `index.html` as the site's home page, so the URL stays clean.)
2. Commit and push.
3. In the repo on GitHub: **Settings → Pages**.
4. Under **Build and deployment → Source**, choose **Deploy from a branch**.
5. Set the branch to **`main`** and the folder to **`/ (root)`**, then **Save**.
6. Wait ~1 minute. Your link appears at the top of the Pages settings, in the form:

   ```
   https://<your-username>.github.io/<repo-name>/
   ```

That link is what you send. (Optional: point a custom domain at it in the same Pages
settings if you'd rather have something like `tee.yourdomain.com`.)

### Suggested repo layout

```
your-repo/
├─ index.html     ← the app (renamed from tee-sheet-builder.html)
└─ README.md      ← this file
```

---

## How to use it (for the golfer)

Open the link in **Safari** on an iPad, then tap **Share → Add to Home Screen** so it opens
like an app. After that:

### First time
1. Open it from the Home Screen icon.

### Every round
1. At the top, type the **round name**, **date**, and **course**.
2. Under **Players**, tap **+ Add a foursome** and type each person's **name** and
   **Course Handicap**. That handicap is the number from the GHIN app's handicap
   calculator — the same lookup you already use.
3. Set each player's **Group** number (Group 1, Group 2, and so on). People in the same
   group share a cart sign. The strokes ("gets 3") are figured out automatically.
4. Optionally add a **tee time or starting hole** for each group.

### Printing
- Tap **Print cart signs** (two per page) or **Print pairing sheet** (the master list).
- In the print screen, pick a printer or choose **Save as PDF** to keep or email a copy.

### Keeping the roster
- The app remembers your list automatically when it's opened from the web link.
- To move it to another device, tap **Copy backup** at the bottom, paste it into a Notes
  entry, then later use **Restore from text** to bring everyone back. You just update the
  handicaps each week and print.

---

## Notes & gotchas

- **Handicaps in, strokes out.** The "gets N" strokes are only as accurate as the Course
  Handicap numbers you enter, so pull fresh numbers from GHIN each round.
- **Persistence needs a URL.** The auto-save (`window.storage`) works when the page is
  served from a web address (GitHub Pages, the Claude app, etc.). If someone opens the raw
  HTML file from the device's file preview, the buttons still work and printing still works,
  but the roster won't be remembered between sessions — that's what the Copy/Restore backup
  is for.
- **No data leaves the device** beyond what your host can see; there's no backend and no
  third-party calls. It does not connect to GHIN — handicaps are typed in by hand.

---

## Tech notes

Plain HTML, CSS, and vanilla JavaScript in one file. No build step, no dependencies, no
framework. Print layout is handled with `@media print` rules; the roster persists via the
host-provided `window.storage` key-value API with a copy/paste fallback for portability.
