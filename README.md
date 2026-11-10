# Gaurav's Garden

A digital garden built with [Quartz v5](https://quartz.jzhao.xyz), published at
https://gauravahujame.github.io/quartz.

## Layout

| Path | What it is |
|---|---|
| `content/` | The notes. Open this folder as the Obsidian vault. |
| `quartz.config.yaml` | Site settings, theme (Flexoki), fonts and plugins. |
| `quartz/styles/custom.scss` | Style tweaks on top of the theme. |
| `.github/workflows/deploy.yaml` | Builds and deploys to GitHub Pages on every push to `v5`. |
| `quartz/` | The Quartz framework itself (from upstream, mostly untouched). |

## Writing

1. Open `content/` as a vault in Obsidian (*Open folder as vault*).
2. In *Settings → Files and links*, set *New link format* to **Shortest path when possible**.
3. Commit and push, either with the Obsidian Git plugin or `npx quartz sync`.

Each note carries a status tag in its frontmatter: `seedling`, `budding` or `evergreen`.

## Local preview

```bash
npm ci
npx quartz build --serve   # http://localhost:8080
```

## Updating Quartz

```bash
npx quartz upgrade   # merges from upstream (jackyzha0/quartz, branch v5)
```

This repo deletes upstream's `docs/`, its workflows and a few GitHub meta files.
If an upgrade reports a modify/delete conflict on one of those, keep the deletion:

```bash
git rm -r docs .github/ISSUE_TEMPLATE   # whichever paths conflicted
git commit
```
