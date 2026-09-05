<!-- BEGIN:nextjs-agent-rules -->

# This is NOT the Next.js you know

This version has breaking changes — APIs, conventions, and file structure may all differ from your training data. Read the relevant guide in `node_modules/next/dist/docs/` (resolved from this file's directory; in monorepos the `next` package may not be visible from the repo root) before writing any code. Heed deprecation notices.

This block is written and re-added by `next dev` — verify at `node_modules/next/dist/server/lib/generate-agent-files.js`. Removing it from a diff only re-creates the uncommitted change; committing it with your work keeps the tree clean.

<!-- END:nextjs-agent-rules -->

# Mandatory: Always use opensrc + installed Next.js docs before implementing

Before implementing any Next.js feature, you MUST ground your work in the installed version's docs and source — NEVER rely on trained data alone.

This repo uses `next@16.3.4` (see `package.json` / `pnpm-lock.yaml`). Training data is stale for this major — APIs, conventions, and file structure have breaking changes.

Required workflow:

1. Resolve the installed source via opensrc (lockfile-aware, cached after first fetch):
   ```powershell
   opensrc path --cwd "E:\learning\use-cache" next
   # e.g. C:\Users\ahmed\.opensrc\repos/github.com/vercel/next.js/16.3.4
   ```
   Use `--cwd` pointing at this repo so `opensrc` picks the locked version, not latest. See https://opensrc.sh/.

2. Read the relevant guide FIRST:
   - Source of truth: `$(opensrc path --cwd . next)/docs/` (`.mdx` source, mirrors `node_modules/next/dist/docs/` `.md` build output)
   - Local build copy: `node_modules/next/dist/docs/` (resolved from this file's directory; in monorepos `next` may not be visible from repo root)
   - Start at `docs/index.md(x)` then `docs/01-app/` (App Router) vs `docs/02-pages/` (Pages Router) + `03-architecture/`.

3. For behavior details, read the implementation in the cached source, e.g.:
   ```powershell
   $NEXT_SRC = opensrc path --cwd "E:\learning\use-cache" next
   Get-ChildItem "$NEXT_SRC\packages\next\src" -Directory
   Get-Content "$NEXT_SRC\packages\next\src\...\*.ts" -TotalCount 100
   ```
   Or search: `rg "use cache" $(opensrc path next)` / `grep -r "Router" $(opensrc path vercel/next.js)/packages/next/src/`.

4. Implement exactly as docs recommend for the installed version. Heed deprecation notices. If docs and your prior knowledge conflict, docs win.

Do not skip steps 1-3 for any `next/*`, App/Pages Router, caching, Server Components, or config task.
