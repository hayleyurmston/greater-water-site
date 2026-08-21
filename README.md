# Greater Water - website deploy guide

A single-page, hand-coded static site. No database, no build step, no server code - which is exactly why it's low-risk to deploy and easy to update.

## What's in this folder

- `index.html` - the whole website (copy, styling, images and structured data are all in this one file)
- `favicon.svg` - the little logo icon that shows in the browser tab
- `robots.txt` - tells search engines they can crawl the site, and where the sitemap is
- `sitemap.xml` - lists the homepage for search engines

Keep all four files together in the root of the repo.

---

## Deploy in the right order (preview first, domain last)

The golden rule: **get it working on Vercel's free preview URL first, then attach the real domain.** You never debug on the public domain.

### 1. Put the files on GitHub
- Create a new repository (e.g. `greater-water-site`), set it to Private.
- Upload the four files in this folder to the repo root (drag-and-drop in the GitHub web uploader is fine).

### 2. Import to Vercel
- In Vercel, click **Add New → Project** and import the GitHub repo.
- Framework preset: **Other** (it's plain HTML). No build command, no output directory needed.
- Click **Deploy**. In a few seconds you'll get a preview URL like `greater-water-site.vercel.app`.

### 3. Check the preview thoroughly
Open the preview URL on both your phone and computer and confirm:
- [ ] Fonts and colours load correctly
- [ ] The truck photo shows in the hero
- [ ] Every "Call" button and the phone number dial `0488 654 416` (test tap-to-call on your phone)
- [ ] All FAQ items open and close
- [ ] Layout looks right on mobile (no overflow, buttons reachable)
- [ ] The sticky "Call Warren" bar appears on mobile

Fix anything here first. To update: change `index.html`, commit to GitHub, and Vercel auto-redeploys in seconds.

---

## Connect the domain (`greaterwater.com.au`)

### 4. Register the domain (NOT through Vercel)
`.com.au` isn't available through Vercel and requires an Australian ABN. Register it at an Australian registrar (VentraIP, Crazy Domains, Netregistry, Synergy Wholesale) using **Warren's business ABN**. Register it in the business's name so Warren owns it.

### 5. Point the domain at Vercel
- In Vercel: **Project → Settings → Domains → Add**, enter `greaterwater.com.au` (and add `www.greaterwater.com.au` too - Vercel will redirect one to the other).
- Vercel shows you the exact DNS records to add (an **A record** for the root, and a **CNAME** for `www`).
- Log in to the registrar, open the domain's DNS settings, and add those records exactly as Vercel lists them.
- Back in Vercel, wait for the domain to verify (usually minutes, sometimes up to a few hours). HTTPS is issued automatically.

Once it verifies, `https://greaterwater.com.au` is live. 🎉

---

## After launch (see also GreaterWater-Project-Notes.md)

- [ ] Google Analytics 4 - create a GA4 property, then paste the snippet into the commented `<!-- Google Analytics 4 ... -->` block near the top of `index.html` (replace `G-XXXXXXX`).
- [ ] Google Search Console - verify the domain, submit `https://greaterwater.com.au/sitemap.xml`.
- [ ] Rich Results Test - run the live URL through search.google.com/test/rich-results to confirm the FAQ + LocalBusiness structured data is valid.
- [ ] Google Business Profile - set as a **service-area business** and **hide the street address** (keeps the family farm private, matches the site).

## Updating the logo or truck photo later

Both are inside `index.html`:
- **Truck photo** - the hero `<img>` uses an inline image. Swap in Warren's high-res original, commit, and Vercel redeploys.
- **Logo** - the header/footer use an inline SVG. Replace with the signwriter's vector when it arrives.

No downtime, no re-launch - visitors just see the updated version on the next load.
