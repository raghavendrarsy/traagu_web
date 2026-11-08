# TRAAGU — Link Hub (GitHub Pages edition)

Same site, rebuilt as a fully static app (React + Vite + Tailwind) that GitHub Pages hosts for free,
plus an **admin panel** at `https://YOUR-SITE/#/admin` for adding/editing releases, shows and site info.

## How the admin works (no server needed)
All content lives in `public/content.json`. The admin panel edits that file and covers/images **directly in
your GitHub repo** using the GitHub API and a personal token. Each publish triggers a rebuild; the change is
live ~1–2 minutes later.

## One-time setup

1. **Create a repo** on GitHub (public — Pages is free for public repos). Upload everything in this folder,
   *including* the hidden `.github/workflows/deploy.yml` (if the web uploader skips it: *Add file → Create
   new file*, name it `.github/workflows/deploy.yml`, paste the contents).
2. **Repo → Settings → Pages → Source: “GitHub Actions”.** Wait for the first run in the *Actions* tab
   (~1 min). Your site is at `https://USERNAME.github.io/REPO/`.
3. **Create an admin token:** GitHub → Settings → Developer settings → Personal access tokens →
   *Fine-grained tokens* → Generate. Repository access: **Only select repositories → this repo**.
   Permissions → Repository → **Contents: Read and write**. Copy the token.
4. Open `https://USERNAME.github.io/REPO/#/admin` (there is also a faint “·” next to the copyright in the
   footer). Paste the token, check owner/repo/branch, **Connect**.
5. **Forms (collab pitch + donate):** Netlify Forms doesn’t exist on GitHub Pages, so these use
   [Web3Forms](https://web3forms.com) (free). Enter `karnatikgang@gmail.com` there, they email you an
   access key, paste it in Admin → Site settings → *Web3Forms access key* → Publish.

## Adding a new release
Admin → Releases → **+ New release**: cover art, title, type (Single/EP/Album), date, description, language,
genre, duration, credits, tracklist, streaming/pre-save links, video link, lyrics. Hit **Add release**,
then **Publish changes**.

* Future date → shown as **Coming soon** on the Latest Release page and in the discography.
* *Draft* hides it from the public site.
* **Latest Release** = newest released Single/EP · **Latest Album** = newest Album.
* Every release gets its own page (`#/release/…`); the **EPK & Song Index** is built automatically from tracklists.

## Security notes
* The token stays in your browser (session only, unless you tick “Remember me”) and is only sent to api.github.com.
* The admin page is public but does nothing without a valid token. Use a token limited to this one repo and
  set an expiry; revoke it on GitHub any time.

## Local development
```bash
npm install
npm run dev     # http://localhost:3000
npm run build   # outputs dist/
```
The two sample releases (“Low Tide Radio”, “Static & Salt”) came from the original source’s placeholder data —
replace or delete them in the admin.
