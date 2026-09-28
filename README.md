# My Heritage Tree — downloads and updates

The download page and the update feed for My Heritage Tree, served by GitHub Pages at <https://mopcweb.github.io/my-heritage-tree-site/>.

Nothing here is written by hand. The app's release workflow publishes into this
repository after every release: it copies the built artifacts into `updates/`, the
installers into `downloads/`, regenerates `index.html`, and force-pushes the result
as one fresh commit — so the repository is only ever as large as its current files.

```
index.html                                 the download page
updates/stable-macos-arm64-update.json     what an installed app checks against
updates/stable-macos-arm64-<name>.app.tar.zst
updates/stable-macos-arm64-<hash>.patch    one per past release, kept for patching
updates/stable-win-x64-...
downloads/my-heritage-tree-<version>-macOS.dmg
downloads/my-heritage-tree-<version>-Windows.exe
downloads/latest.json                      version, date and file names, for the page
```

An installed app fetches `updates/<platform>-update.json`, compares the hash with
its own, and downloads the patch or the whole archive from the same folder. The
files under `updates/` keep the names Electrobun gave them; renaming any of them
breaks updating.

## Setting up once

1. Settings → Pages → Build and deployment → Source: **GitHub Actions**.
2. In the app repository, add a secret `SITE_DEPLOY_TOKEN`: a fine-grained personal
   access token with *Contents: read and write* on this repository only.
3. Release the app. The first release to land here is the one people download; the
   apps it installs update themselves from then on.
