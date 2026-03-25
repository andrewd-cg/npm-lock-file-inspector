# npm Lock File Inspector

A zero-dependency, single-file web app for inspecting and comparing `package-lock.json` files. Built for comparing public npm registry dependencies against [Chainguard](https://www.chainguard.dev/) library mirrors.

## Usage

Open `index.html` directly in a browser — no server, no build step required.

### Single file mode

Drop or upload one `package-lock.json` to see a sortable, searchable table of all resolved dependencies showing:

- Package name (links to npmjs.com)
- Version
- Resolved URL
- License

### Compare mode

Drop a second `package-lock.json` to diff the two files. Tabs break down the results into:

| Tab | Description |
|-----|-------------|
| **Version Changed** | Packages present in both files but at different versions |
| **Only in File A** | Packages unique to the first file |
| **Only in File B** | Packages unique to the second file |
| **Same Version** | Packages resolved identically, with both URLs shown side-by-side |
| **All Packages** | Full combined view with status badges |

## Chainguard registry indicators

Packages resolved from `libraries.cgr.dev` are automatically tagged in the resolved URL column:

| Badge | Path | Meaning |
|-------|------|---------|
| 🔒 secured | `/javascript/` | Chainguard Built |
| ↑ upstream | `/javascript-upstream/` | Chainguard cache, 7 day cooldown & Malware scanned |

The stats bar also shows a count of secured vs upstream packages across the file.

## Supported lockfile versions

| Version | npm version | Notes |
|---------|------------|-------|
| v1 | npm 5/6 | Parsed from `dependencies` tree |
| v2 | npm 7+ | Parsed from `packages` block (hybrid format) |
| v3 | npm 7+ | Parsed from `packages` block |

License data is available in v2/v3 lockfiles only.
