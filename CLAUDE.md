# Surgical Sledgehammer Lite

Lightweight static portfolio site for Surgical Sledgehammer LLC. Replaces the old Laravel version. Vite + Tailwind CSS + Alpine.js, outputs pure static HTML for S3 hosting.

## Pages

- `/` — Home with hammer-to-sword SVG animation, stream-of-consciousness pitch, "Hire me" CTA
- `/portfolio.html` — Vimeo video embed ("I'm Jason and I Exist")
- `/contact.html` — Just email: jason@jasonhorsley.tech
- `/graphable/` — Nav link only. Graphable is a separate app (cultural-shift-graphs repo) deployed independently to the same S3 bucket.

## Deploy

The site is hosted on S3 bucket `surgicalsledgehammer.com` behind CloudFront distribution `EC143K560K4AQ`.

```bash
npm run build
aws s3 sync dist/ s3://surgicalsledgehammer.com/ --exclude "graphable/*"
aws cloudfront create-invalidation --distribution-id EC143K560K4AQ --paths "/*"
```

**Do NOT use `--delete` on the s3 sync.** The `graphable/` folder and its assets (in `assets/`) are deployed separately from the cultural-shift-graphs repo. Using `--delete` will wipe those files. If you must use `--delete`, redeploy graphable at the same time.

## Dev

```bash
npm install
npm run dev
```
