# ZeroBusyWork site

A simple multi-ebook static site. No build tools, no framework — just
HTML/CSS, so it's easy to hand-edit and cheap to host.

```
/index.html                          → homepage, lists all ebooks
/assets/style.css                    → shared design (colors, fonts, layout)
/ebooks/hr-copilot-for-hr-admin/     → your first ebook's page
/ebooks/_template/                   → duplicate this for every new ebook
```

---

## One-time setup: move from Netlify Drop to GitHub auto-deploy

Right now your site is deployed by dragging a folder onto Netlify by hand.
Do this once and every future update deploys itself.

### 1. Create a GitHub account (skip if you already have one)
Go to https://github.com/join and sign up — it's free.

### 2. Create a new repository
- Go to https://github.com/new
- Repository name: `zerobusywork-site` (or anything you like)
- Keep it **Public** or **Private** — either works with Netlify
- Don't add a README/gitignore/license (we already have files) — just click **Create repository**

### 3. Upload this folder to the repository
On the new repo's page:
- Click **"uploading an existing file"** (or Add file → Upload files)
- Drag this entire `zerobusywork-site` folder's contents into the upload box
  (drag the *contents* — index.html, assets/, ebooks/, this README — not the
  outer folder itself)
- Scroll down, click **Commit changes**

No command line needed — GitHub's website handles this entirely by drag-and-drop,
same as Netlify Drop did.

### 4. Connect the repo to your existing Netlify project
- In Netlify, open your **zerobusywork** project
- Go to **Site configuration → Build & deploy → Continuous deployment**
- Look for an option like **"Link repository"** or **"Link site to Git"**
- Choose **GitHub**, authorize Netlify to access your account (you'll get an
  OAuth permission prompt from GitHub — this is normal and needed so Netlify
  can pull your files)
- Pick the `zerobusywork-site` repository
- Build settings: leave **Build command** blank and set **Publish directory**
  to `.` (a single dot) since this is a plain static site with no build step
- Click **Deploy**

From now on, any change you push to the GitHub repo automatically redeploys
your live site within a minute or two — no more dragging folders.

---

## Adding a new ebook (do this every time you launch one)

1. **Duplicate the template folder.** Copy `/ebooks/_template/` and rename
   the copy to your new ebook's slug, e.g. `/ebooks/copilot-for-sales/`
   (lowercase, hyphens, no spaces — this becomes part of the URL).

2. **Fill in the page.** Open the new folder's `index.html` and replace every
   `{{PLACEHOLDER}}` with your real copy. Delete the instructions comment at
   the top once done.

3. **Add the Razorpay button.** In your Razorpay Dashboard → Payment Buttons,
   create a button for this product, copy its embed snippet, and paste it
   where the template marks `RAZORPAY PAYMENT BUTTON GOES HERE`.

4. **Add it to the homepage.** In `/index.html`, copy one of the existing
   `<a class="book-card">` blocks inside `<div class="catalog-grid">`, point
   its `href` at your new ebook's folder, and update the eyebrow/title/blurb/price.
   Remove the "Coming Soon" placeholder card if you don't want it anymore.

5. **Push the changes to GitHub** (via the web upload flow, same as step 3
   in setup above, or `git push` if you're comfortable with git). Netlify
   redeploys automatically — check the **Deploys** tab on your Netlify
   project to confirm it went live.

That's the whole loop: duplicate → fill in → add Razorpay button → link from
homepage → push. No coding beyond editing text between the existing HTML tags.

---

## Notes

- All pages share one stylesheet (`/assets/style.css`), so if you ever want
  to tweak the color scheme or fonts site-wide, change it once there.
- The `.coming-soon` card style on the homepage is there if you want to tease
  an upcoming ebook before it's ready — see the example in `/index.html`.
- Keep ebook slugs short and readable — they're the actual page URL, e.g.
  `zerobusyworkbooks.com/ebooks/copilot-for-sales/`.
