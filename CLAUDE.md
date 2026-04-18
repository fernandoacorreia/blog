# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this repo is

A Hugo static site (Fernando Correia's blog) that publishes to GitHub Pages. Source lives here; the rendered site lives in the `public/` submodule.

## Commands

All commands are bash wrappers in `bin/`. Hugo runs inside a Docker image — no Hugo install on the host.

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

## Draft workflow

Posts default to `draft: true` in the archetype. Drafts are **rendered by `bin/server`** (it passes `-D`) but **excluded from the production build** (called by `bin/publish`). Flip `draft: false` before publishing.
