# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this repo is

A Hugo static site (Fernando Correia's blog) that publishes to GitHub Pages. Source lives here; the rendered site lives in the `public/` submodule.

## Commands

All commands are bash wrappers in `bin/`. Hugo runs inside the `hugomods/hugo:dart-sass-0.160.1` Docker image (Hugo Extended 0.160.1 + Dart Sass — required by the `hugo-clarity` theme's SCSS) — no Hugo install on the host.

| Command | What it does |
|---|---|
| `bin/hugo new posts/{slug}.md` | Scaffolds a post from `archetypes/posts.md` with `draft: true`. |
| `bin/server` | Dev server at http://localhost:1313/ with `-D` (drafts included) and live reload. Ctrl+C to stop. |
| `bin/publish "commit msg"` | Builds + publishes. See "Publish flow" below. |
| `bin/date` | UTC timestamp in front-matter format. |

## Publish flow

`bin/publish` is the **only** path to production. It:

1. Runs hugo to build into `public/`.
2. `cd public && git add . && git commit && git push origin master` — this publishes the site (GitHub Pages auto-serves from this repo).
3. `cd ..` and commits/pushes the blog source repo.

So the site goes live as soon as step 2 pushes. If step 3 fails, the source repo is out of sync with what's live — re-run or push manually.

### Before publishing

- Stop `bin/server` if it's running. `bin/publish` builds via `bin/hugo`, which binds port 1313 and will fail with `Bind for 0.0.0.0:1313 failed: port is already allocated` if the dev server is up.

### Verify the publish actually happened

After `bin/publish`, the push line for the public repo (step 2) must show a `sha1..sha2  master -> master` range. If it says `Everything up-to-date`, **the site did not publish** — the `public/` submodule was on detached HEAD, the new commit is orphaned, and stale local `master` was pushed instead.

### Recovery: detached HEAD in `public/`

The `public/` submodule frequently sits on detached HEAD (git's default when a parent repo records a submodule at a specific SHA). That's the root cause of the failure above. Recovery recipe is in README.md under "Publish changes to GitHub Pages"; reproduced here so you can run it without switching files:

```
cd public
git push origin HEAD:master
git checkout master
git fetch --all
git reset --hard origin/master
```

You are pre-authorized to run this recipe when the publish verification fails. It is non-destructive: it fast-forwards `origin/master` to the just-built HEAD, then re-syncs the local `master` branch to match.

## Draft workflow

Posts default to `draft: true` in the archetype. Drafts are **rendered by `bin/server`** (it passes `-D`) but **excluded from the production build** (called by `bin/publish`). Flip `draft: false` before publishing.
