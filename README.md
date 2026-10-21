# bluebeauty-digital

The public web address of the Garmin watch face **Blue Beauty Earth Digital**:

| Page | URL |
|---|---|
| Share link (redirects to the Connect IQ Store) | https://leidenheit.github.io/blue-beauty-earth-digital-static/ |
| Requirements (devices, features, permissions) | https://leidenheit.github.io/blue-beauty-earth-digital-static/hardware-requirements.html |
| License | https://leidenheit.github.io/blue-beauty-earth-digital-static/license.html |

The watch face ships the first address: as the share link in its phone
settings and as the QR code in its on-watch menu. The Store entry's
description links to the requirements page.

The analog face has its own site, built the same way:
https://leidenheit.github.io/blue-beauty-earth-analog-static/ (repo
leidenheit/blue-beauty-earth-analog-static, checked out as `../bluebeauty`).

## Why a redirect

Garmin assigns the store page's id when an entry is first uploaded, and the
beta and the release are separate entries. So the release page's address cannot
be known before the release upload, and the beta page is visible only to the
account that uploaded it. The face therefore links here, and only the target of
this redirect changes.

## The one setting: `store_url` in `_config.yml`

| Phase | `store_url` | What the share link does |
|---|---|---|
| Before the first upload | `""` (empty) | shows a landing page: picture, name, "coming soon", links |
| Beta test | the beta entry's page | forwards there (only the uploading account can open it) |
| Garmin review | `""` (empty) | shows the landing page |
| Released | the release entry's page, from the developer dashboard | forwards there |

During the review the page must not forward to the beta page: Garmin's review
guidelines ask for "no broken links", and the reviewer cannot open the beta.

Edit the line, commit and push. GitHub Pages rebuilds within about a minute. A
new watch package is never needed for this.

## Rules

- **The address never changes.** An installed watch face keeps the share link
  it was installed with. Do not rename the repo, do not move the site, and keep
  the trailing slash. Without it, GitHub first redirects to the address
  with the slash.
- **The site stays online** as long as the watch face is in the store.
- Three parts of `hardware-requirements.md` are generated; change them in the
  watch face repo (blue-beauty-digital-watchface-garmin) with
  `python tools/make_pages_devices.py`. It writes the watch table (from
  `manifest.xml` and the SDK), the languages each watch shows in English, and
  the figures of the turning Earth (frames, seconds, degrees, read from
  `tools/render_scrolling_planet_animations.py`) between their marker comments.
  After a change to the renderer, rebuild the planet assets (`build.ps1 -DRes`
  per resolution) as well, or the watch keeps playing the old animation while
  this page already describes the new one.
- `assets/face.png` (340 x 340, the lit face on the page's black) and
  `assets/icon-128.png` are pictures of the digital face. Replace them with the
  store icon and the store picture once those exist.

## Setup (once)

1. Create the **public** repo `leidenheit/blue-beauty-earth-digital-static` on
   GitHub. Pages is free only for public repos.
2. In this folder: `git init -b main`, commit everything, then
   `git remote add origin https://github.com/leidenheit/blue-beauty-earth-digital-static.git`
   and `git push -u origin main`.
3. On GitHub, open Settings > Pages and set Source to "Deploy from a branch",
   Branch `main`, folder `/ (root)`.
4. After 1-2 minutes open https://leidenheit.github.io/blue-beauty-earth-digital-static/
   on the PC and on the phone. Both must show the landing page (or, with
   `store_url` set, land on the store page).

## License

Copyright 2026 Attila "leidenheit" Varga. All rights reserved, see
[LICENSE](LICENSE). That covers the watch face and the content of this site.
The repository is public only because GitHub Pages is free for public
repositories; being readable does not make it open source.
