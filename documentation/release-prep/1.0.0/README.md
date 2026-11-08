# slot.advance 1.0.0: release preparation

*Historical record of the 1.0.0 release preparation (Phase 7), kept as for 0.5.0. Not user documentation. These notes were written on the `docs/1.0.0-release-prep` branch; the sections below describe that branch as it stood before publication.*

**Released (8 November 2026):** slot.advance 1.0.0 was published and verified. See [Publication](#publication).

**Status before publication (8 November 2026):** Phase 7 review approved with final corrections, all made on this branch: the README bullet's progress sentence, the webpki-roots licence and release-workflow licence checks, the vendored rcheevos description, the comparison with upstream slot 1.15.1, and the version set to 1.0.0. Built on `release-0.6.0` at `08261fd`, the code tested on the handheld in Phase 6. At that point nothing was merged, tagged, released, deployed or published.

## Publication

- **Release tag:** `advance-1.0.0`
- **Release commit:** `7f68f6430a0f6593afbe64939d95c3a10f6ae597` (`docs/1.0.0-release-prep` fast-forwarded into `release-0.6.0`; no runtime change from `08261fd`)
- **Release:** [slot.advance 1.0.0](https://github.com/slowphase/slot.advance/releases/tag/advance-1.0.0), published by the release workflow (run 42446896781, build and publish jobs both successful) and marked Latest, with `documentation/releases/advance-1.0.0.md` as its notes.
- **Asset:** `slot.advance-1.0.0-rg-sp.zip`, 15,581,000 bytes, SHA-256 `d3fd417b15741afe282631ed6595a6aab91875a978fa464d9fe70a4fcec04eef`.
- **Verified after publishing:** the download link works; the archive tests clean; its single top folder `slot.advance-1.0.0-rg-sp/` holds the SD2 tree (`BIOS`, `Config`, `Games`, `Labels`, `Saves`, `States`, `System`, `Wallpapers`); `System/slot` (version 1.0.0), both cores and Syncthing are aarch64; `System/licenses/` holds `rcheevos-MIT.txt` and `webpki-roots-CDLA-Permissive-2.0.txt`, identical to the copies at the release commit (webpki-roots 1.0.11).

## What this branch contains

`release-0.6.0` (`08261fd`) plus documentation, screenshots, charts and their generators, and the approved release packaging changes. No runtime change: outside documentation, `git diff 08261fd <this branch>` lists only the version (`Cargo.toml`, the ten workspace crates in `Cargo.lock`), `licenses/webpki-roots-CDLA-Permissive-2.0.txt`, the licence checks in `.github/workflows/release.yml`, comments in `crates/slot-achievements/build.rs` and `vendor/README.md`, and `crates/slot/examples/readme_100_screenshots.rs` (an example, not built into the release).

| Area | Files |
|---|---|
| README | `README.md`: one RetroAchievements feature bullet, the two-bar battery chart and its paragraph, the 1.0.0 version and download links, the RetroAchievements and rcheevos credit |
| User guide | `documentation/user-guide.md`: a RetroAchievements section, plus Settings, files, going back, troubleshooting, limitations, reporting and the comparison with slot |
| Technical reference | `documentation/technical.md`: a RetroAchievements section, plus the intro, architecture, lid close, Power Off and Restart, security, performance, logging, limitations and source map |
| Sleep and battery | `documentation/sleep-and-battery.md` (a 1.0.0 section and validation status; history unchanged), `documentation/battery-tests/` (`charts.py`, new `calculate-1.0.0.py`) |
| Release notes | `documentation/release-notes.md` (1.0.0 section, version-number note) |
| GitHub Release text | `documentation/releases/advance-1.0.0.md`. The release workflow publishes this file **from the tagged commit**, verbatim |
| Charts | `.github/resources/battery/battery-standby-1.0.0.svg` (README) and `battery-awake-ra-1.0.0.svg` (sleep and battery). Every earlier chart regenerates byte for byte unchanged |
| Screenshots | `.github/resources/screenshots/advance/1.0.0/` (with a README on how each was made) |

## How the battery evidence is presented

- **The README's chart** compares semi-stock software standby (~7% an hour, Test B) with slot.advance 1.0.0 (~2% an hour). The 1.0.0 bar is not labelled projected or estimated; a note on the chart and in the text says it comes from the two extended 8-hour 0.5.0 sleeps (V1-B, V1-D) of the same hardware sleep implementation. Nothing says a sleep was measured on 1.0.0.
- **The 0.4.x and 0.5.0 history is unchanged** in `sleep-and-battery.md`, and the earlier README chart (`battery-drain-hourly.svg`) is still generated, unchanged, as the release-by-release record.
- **RetroAchievements while playing:** 494 against 503 mA, +9 mA (+1.8%), standard error 6, within measurement noise; both runs Wi-Fi On, 80% to 71%; described as the observed difference, not a maximum; not compared with 0.5.0's figures; plainly an active-play measurement.

## Not claimed anywhere

- Partial progress across a cold-boot resume on the handheld (host tests only; stated as a limitation).
- Any sleep or standby measurement on a 1.0.0 build.
- A same-night or Wi-Fi Off RetroAchievements battery pair.

## Release checklist

**Completed 8 November 2026.** Kept as written, with each step's outcome noted. Each step needed Dean's explicit approval at the release checkpoint.

1. **Review** this branch (with ChatGPT if wanted). *Done: Phase 7 approved.*
2. **Version: done on this branch.** `Cargo.toml` and the ten workspace crates in `Cargo.lock` say 1.0.0; the RetroAchievements user agent reads `slot.advance/1.0.0 (Linux aarch64) rcheevos/12.5.0`. Host tests, fmt and clippy pass (the same three environment-only test failures as at Checkpoint D). *Done.*
3. **Into the release branch:** merge `docs/1.0.0-release-prep` into `release-0.6.0`, so the tagged commit carries the version, the licences, the workflow checks and `documentation/releases/advance-1.0.0.md`. *Done: fast-forward to `7f68f64`.*
4. **Check the tagged tree:** `Cargo.toml` says 1.0.0; `git diff 08261fd <commit> -- crates cores card scripts taskfile.yml` shows only the version lines, the two comment corrections and the screenshot example; `.github/workflows/release.yml` only the licence checks. *Done: no change under `crates/*/src`, `card`, `cores` or `scripts`. A non-publishing run of the release workflow from `release-0.6.0` also passed, including the artifact upload.*
5. **Tag and publish:** tag `advance-1.0.0` (or run the release workflow by hand with `release_tag` `advance-1.0.0`). The README's download link (`releases/download/advance-1.0.0/slot.advance-1.0.0-rg-sp.zip`) works only once this is published. *Done: published by running the workflow with `release_tag` `advance-1.0.0`; the tag points at `7f68f64`.*
6. **After publishing:** download the asset through the README's link, check the top folder `slot.advance-1.0.0-rg-sp` and that `System/licenses/` holds `rcheevos-MIT.txt` and `webpki-roots-CDLA-Permissive-2.0.txt` (the workflow now fails without them); note the asset's SHA-256. *Done: see [Publication](#publication).*
7. **main:** merge `release-0.6.0` into `main` (separate approval). *Done 8 November 2026, after publication, as a fast-forward, together with the 1.0.0 README hero image.*
8. **Website:** slotadvance.com still shows the 0.5.0 battery blocks and copy (separate approval). *Done: updated separately.*
