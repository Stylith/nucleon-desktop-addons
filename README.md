Nucleon Desktop First-Party Optional Addons Repository

This directory is the staged contents for the future standalone `nucleon-desktop`
first-party addons repository.

Current purpose:
- host optional first-party addon manifests outside the core shell repo
- publish a repository index consumable by the installer feed
- keep shell-critical addons in the main repo while optional addons move out first

Current optional addons staged here:
- `games.red-menace`
- `games.zeta-invaders`
- `tools.nuke-codes`

Bundle format:

- each addon bundle contains `manifest.json`
- shell-hosted WASM addons also contain an `addon.wasm` module
- additional assets/data files live beside those files inside the same addon directory

Repository layout:
- `index.json` — addon manifests, release metadata, and `base_url` for downloads
- `games/*.ndpkg` — game addon packages
- `tools/*.ndpkg` — tool addon packages

Current artifact contract:
- artifact format is `ndpkg` (renamed ZIP archive)
- artifact URL is a filename relative to the index `base_url` (raw GitHub content)
- installer downloads the `.ndpkg` archive directly from this repo, verifies SHA-256, extracts via the `zip` crate
- to update an addon: replace its `.ndpkg` file, update the sha256 in `index.json`, push
- installed addon is still hosted inside the shell UI rather than launching as a separate OS window

Not included yet:
- packaged binaries
- dynamic plugin loading
- third-party trust model
- signed update workflow
