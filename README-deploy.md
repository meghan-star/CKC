# Crystal Kitty Club — Deployment Guide

## Site stack
Same setup as RemindZen: HTML files → GitHub repo → Cloudflare Pages (free hosting)

---

## Step 1 — Create GitHub repo

1. Go to github.com → New repository
2. Name it `crystalkittyclub` (or `crystalkittyclub.com`)
3. **Set to Public** (required for free Cloudflare Pages)
4. Don't initialize with README (you already have files)
5. Create repository

---

## Step 2 — Upload files

Upload the entire `crystalkittyclub-site` folder contents to the repo root:

```
/                       ← repo root
├── index.html
├── gallery.html
├── quiz.html
├── wallpapers.html
├── styles.css
├── sitemap.xml
├── robots.txt
└── images/
    ├── opal-rainbow.png
    ├── diamond-palace.png
    ├── crystal-throne.png
    ├── moonlit-pearl.png
    ├── cosmic-moon.png
    ├── pink-cloud.png
    └── emerald-forest.png
```

**Image naming is exact — filenames must match exactly as listed above.**
All images go inside the `images/` subfolder.

---

## Step 3 — Connect Cloudflare Pages

1. Go to Cloudflare Dashboard → Pages → Create a project
2. Connect to Git → select your GitHub repo
3. Build settings: **leave blank** (static site, no build command needed)
4. Deploy → Cloudflare gives you a `*.pages.dev` URL
5. Add custom domain: `crystalkittyclub.com`
6. Update your domain registrar's nameservers to point to Cloudflare (same process as RemindZen)

---

## Step 4 — Set up Formspree (email capture)

The site has two email forms — both need the same Formspree ID replaced.

1. Go to formspree.io → sign up free
2. Create a new form → name it "Crystal Kitty Club"
3. Copy the form ID (looks like: `xpzvjkqr`)
4. In these two files, find `REPLACE_WITH_YOUR_ID` and replace with your actual ID:
   - `index.html` (quiz CTA section)
   - `quiz.html` (oracle summon form)
   - `wallpapers.html` (wallpaper waitlist)

Example: `action="https://formspree.io/f/xpzvjkqr"`

---

## Step 5 — Add Instagram and Pinterest URLs

Once accounts are set up, find `href="#"` in these files and replace with real URLs:

In `index.html`, `gallery.html`, `quiz.html`, `wallpapers.html`:
```html
<!-- Instagram — replace # -->
<a href="https://instagram.com/crystalkittyclub" ...>

<!-- Pinterest — replace # -->
<a href="https://pinterest.com/crystalkittyclub" ...>
```

---

## Step 6 — Submit to Google

Once the site is live at crystalkittyclub.com:

1. Go to Google Search Console → Add property → URL prefix → enter `https://crystalkittyclub.com`
2. Verify ownership via Cloudflare DNS TXT record (Cloudflare makes this easy)
3. Submit sitemap: paste `https://crystalkittyclub.com/sitemap.xml` in the Sitemaps section
4. Request indexing on the URL inspection tab for each page

Google should index within 1–4 weeks. The sitemap and robots.txt are already set up correctly.

---

## Adding new queens to the gallery

When you have new cat images to add:

1. Save the image as a lowercase, hyphenated filename (e.g., `amethyst-throne.png`)
2. Upload to the `images/` folder in your GitHub repo
3. In `gallery.html`, find the comment block `<!-- Add new gallery items here -->` and add:

```html
<div class="gallery-item">
  <img src="images/amethyst-throne.png" alt="Amethyst Throne Queen — [describe the image]" loading="lazy">
  <span class="gallery-label">Amethyst Throne</span>
</div>
```

4. Also add to `index.html` gallery preview section (optional — keep it to 6 featured)
5. Commit and push → Cloudflare auto-deploys in ~30 seconds

---

## Updating sitemap dates

When you make major updates (new queens, quiz launch), update the `<lastmod>` dates in `sitemap.xml`.

---

## Cost summary

| Item | Cost |
|------|------|
| Domain (crystalkittyclub.com) | ~$11/year |
| GitHub | Free |
| Cloudflare Pages | Free |
| Formspree (up to 50 submissions/month) | Free |
| **Total** | **~$11/year** |
