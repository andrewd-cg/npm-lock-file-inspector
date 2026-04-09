# npm Lock File Inspector

A zero-dependency, single-file web app for inspecting and comparing lock files. Built for comparing public npm registry dependencies against [Chainguard](https://www.chainguard.dev/) library mirrors.

## Usage

Open `index.html` directly in a browser — no server, no build step required.

### Single file mode

Drop a lock file into the **npmjs** slot to see a sortable, searchable table of all resolved dependencies:

- Package name (links to npmjs.com)
- Version
- Resolved URL
- License

### Compare mode

Drop a lock file into each slot to diff them side by side. The left slot is assumed to be your **npmjs** lock file and the right slot your **Chainguard** lock file — resolved URLs are inferred from this when not explicitly stored in the lockfile (e.g. Yarn Berry).

Tabs break down the results into:

| Tab | Description |
|-----|-------------|
| **Version Changed** | Packages present in both files but at different versions |
| **Only in npm** | Packages unique to the npmjs lock file |
| **Only in Chainguard** | Packages unique to the Chainguard lock file |
| **Same Version** | Packages resolved identically, with both URLs shown side-by-side |
| **All Packages** | Full combined view with status badges |

### Export snapshot

Click **Export snapshot** in the toolbar to download a self-contained HTML file with all package data embedded. Recipients can open it directly in a browser to view, search, and browse the results — no lock files needed.

## Chainguard registry indicators

Packages resolved from `libraries.cgr.dev` are automatically tagged in the resolved URL column:

| Badge | Path | Meaning |
|-------|------|---------|
| 🔒 secured | `/javascript/` | Chainguard Built |
| ↑ upstream | `/javascript-upstream/` | Chainguard cache, 7 day cooldown & Malware scanned |

The stats bar shows a count of secured vs upstream packages across the file.

## Supported lock file formats

| Format | Notes |
|--------|-------|
| `package-lock.json` v1 | npm 5/6 — parsed from `dependencies` tree |
| `package-lock.json` v2/v3 | npm 7+ — parsed from `packages` block. Includes license data |
| `yarn.lock` v1 | Classic Yarn — includes resolved registry URLs |
| `yarn.lock` Berry (v2–v4) | Resolved URLs extracted from `__archiveUrl` where present, otherwise inferred from slot position |
