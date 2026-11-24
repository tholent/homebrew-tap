# homebrew-tap

tholent's [Homebrew](https://brew.sh) tap: every cask and formula tholent makes, in one place.

| Install | What it is |
|---|---|
| `brew install --cask tholent/tap/quadrule` | [Quadrule](https://github.com/tholent/quadrule), a free, open-source design tool for Supernote page templates and wallpapers (macOS) |

`brew upgrade` moves each one to its newest release.

Homebrew 6 runs nothing from a tap you have not trusted. Installing by the full name, as above, trusts that one cask
or formula and nothing else in the tap ([Tap Trust](https://docs.brew.sh/Tap-Trust)).

Quadrule is not signed by Apple yet, so macOS warns the first time you open it. Open it once and close the warning,
then go to System Settings → Privacy & Security and click **Open Anyway** next to the message about Quadrule.

## How this tap is kept

- Casks (Mac apps) live in `Casks/`, formulas (command-line programs) in `Formula/`, one file each.
- A project that releases on its own writes its own file here from its release workflow, with a deploy key that can
  write to this repository. Change such a file in its project, not here: the next release overwrites it.
  - `Casks/quadrule.rb`: source `packaging/homebrew/quadrule.rb` in
    [tholent/quadrule](https://github.com/tholent/quadrule) (quadrule's ADR-025).
- A cask whose releases are all GitHub pre-releases (Quadrule, until its 1.0) is listed in
  `audit_exceptions/github_prerelease_allowlist.json` with `"any"`, so `brew audit` accepts its pre-releases and,
  later, its full releases.
- `.github/workflows/check.yml` runs `brew style` and `brew audit` on every cask and formula after each change, and
  installs and uninstalls each cask on a Mac.
