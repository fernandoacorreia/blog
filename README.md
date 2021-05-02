# blog

Fernando Correia's Blog.


## Instructions

### Cloning

This repository uses submodules.

Clone it with submodules:

```
git clone --recurse-submodules git@github.com:fernandoacorreia/blog.git
```

Or update submodules after cloning:

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

### Start local server

```
bin/server
```

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
bind/date
```
