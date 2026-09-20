# ParkourPro Wiki

Documentation for **ParkourPro** and **ParkourPro Lite** (Minecraft 1.8 – 26.x).

- `docs/` – the website for **GitHub Pages** (`docs/index.html`, single page with search, edition switch and command reference).
- `wiki/` – Markdown pages for the **GitHub Wiki** tab (`Home.md`, `Commands.md`, ... plus `_Sidebar.md`).

## Publish the website (GitHub Pages)

1. Create a repository on GitHub, for example `ParkourPro-Wiki`, and push this folder:

   ```bash
   git remote add origin https://github.com/stanotermans/Parkourpro-lite-wiki.git
   git push -u origin main
   ```

2. On GitHub open **Settings → Pages**. Under *Build and deployment* choose **Deploy from a branch**, branch `main`, folder `/docs`, and save.
3. After a minute the site is live at `https://stanotermans.github.io/Parkourpro-lite-wiki/`.

## Publish the wiki pages (GitHub Wiki tab)

1. In the repository open the **Wiki** tab and click **Create the first page** (any content, this initialises the wiki).
2. Clone the wiki repository and copy the pages:

   ```bash
   git clone https://github.com/stanotermans/Parkourpro-lite-wiki.wiki.git
   cp wiki/*.md Parkourpro-lite-wiki.wiki/
   cd Parkourpro-lite-wiki.wiki
   git add . && git commit -m "ParkourPro wiki 1.0.9" && git push
   ```

The sidebar (`_Sidebar.md`) and footer are picked up automatically.

## Updating

Edit the Markdown in `wiki/` (and copy it to `docs/wiki/`) or `docs/index.html`, commit and push. Pages redeploys automatically.
