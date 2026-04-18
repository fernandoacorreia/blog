# blog

Fernando Correia's Blog.


## Prerequisites

- [Docker](https://www.docker.com/) — `bin/hugo` and `bin/server` run Hugo inside the `klakegg/hugo:0.74.3-ext-alpine` container, so nothing needs to be installed on the host. Make sure the Docker daemon is running.
- Git — for cloning, submodules, and publishing.
- Bash — for the helper scripts in `bin/`.


## Instructions

### Cloning

This repository uses two submodules:

- `themes/hugo-clarity` — the Hugo theme. **Required:** without it every page renders as an empty `<pre></pre>` with no error.
- `public/` — the GitHub Pages publish target (`fernandoacorreia.github.io`), used by `bin/publish`.

Clone with submodules:

```
git clone --recurse-submodules git@github.com:fernandoacorreia/blog.git
```

Or, if you already cloned without `--recurse-submodules`:

```
git submodule update --init --recursive
```

### Run hugo

```
bin/hugo
```

### Create a new post

```
bin/hugo new posts/{file-name}.md
```

The post is created from `archetypes/posts.md` with `draft: true` in the front matter. See [Draft workflow](#draft-workflow) below.

### Start local server

```
bin/server
```

Serves the site at http://localhost:1313/ with live reload. Drafts are included (the script passes `-D`).

### Stop local server

Press `Ctrl+C` in the terminal running `bin/server`. The container is started with `--rm`, so it's removed on exit.

### Draft workflow

New posts start with `draft: true`. Drafts:

- **Are** rendered by `bin/server` (runs Hugo with `-D`).
- **Are not** included in production builds — `bin/publish` skips them.

Set `draft: false` in the post's front matter when you're ready to publish.

### Publish changes to GitHub Pages

```
bin/publish {commit description}
```

If the publication gets stuck and is not uploaded to the [github.io repo](https://github.com/fernandoacorreia/fernandoacorreia.github.io) try this:

```
cd public
git push origin HEAD:master
git checkout master
git fetch --all
git reset --hard origin/master
```

### Other useful commands

Display current timestamp in a format compatible with blog article metadata:

```
bin/date
```
