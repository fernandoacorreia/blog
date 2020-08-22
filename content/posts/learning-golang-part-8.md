---
title: "Learning Golang: Running Go in a container" # Title of the blog post.
date: 2020-08-22T01:55:41Z # Date of post creation.
tags: ["golang"]
categories: ["learning golang"]
# description: "Article description." # Description used for search engine.
# featured: true # Sets if post is a featured post, making appear on the home page side bar.
# toc: false # Controls if a table of contents should be generated for first-level links automatically.
# menu: main
# featureImage: "/images/path/file.jpg" # Sets featured image on blog post.
# thumbnail: "/images/path/thumbnail.png" # Sets thumbnail image appearing inside card on homepage.
# shareImage: "/images/path/share.png" # Designate a separate image for social media sharing.
# codeMaxLines: 10 # Override global value for how many lines within a code block before auto-collapsing.
# codeLineNumbers: false # Override global value for showing of line numbers within code block.
# figurePositionShow: true # Override global value for showing the figure label.
# categories:
#   - Technology
---

This is part 8 of my [journey](/categories/learning-golang/) learning Golang.


# Reproducible build & run environments

Over the years, it is not uncommon that different projects in the same language will have different requirements about
the versions of the tools and libraries that they require.

For instance, I learned that there are differences in the behavior of the `GO111MODULE` environment variable
across Go versions 1.12 and 1.13.

That's why when I start a repository for a new project, one of the first things I do is to set up scripts for building
and running the code in a reproducible way.

Docker containers are a very effective tool for that. So when I created a GitHub repo for my
[learning-go](https://github.com/fernandoacorreia/learning-go) project, I set up a quick script to run the code. This
way I know I'll be able to run it years from now without any special setup other than having Docker installed.

I wish this was a general practice for open source projects. Getting their build requirements installed can be a chore,
particularly when there are version conflicts with other projects.


# Running Go in a Docker container

This is the script that I'm using for running my first Go programs:

```bash
#!/bin/bash
#
# Runs Go.
#
set -o nounset -o errexit -o pipefail                     # Abort the script on errors

SCRIPT_DIR=$(cd "$(dirname "${BASH_SOURCE[0]}")" && pwd)  # Absolute directory where this script is stored
BASE_DIR=$(cd "$SCRIPT_DIR/.." && pwd)                    # Parent directory of this script
GO_VERSION="1.15-buster"                                  # Docker image tag of the Go version that will be used

mkdir -p "$BASE_DIR/.cache"                               # Create .cache directory under base directory

docker run                       `# Run a Docker container                               ` \
  --rm                           `# Remove the container when the command exits          ` \
  -it                            `# Set an interactive terminal                          ` \
  -v "$BASE_DIR":"$BASE_DIR"     `# Mount base directory with same name in the container ` \
  -v "$BASE_DIR/.cache":/.cache  `# Mount .cache directory under the container's root    ` \
  -w "$BASE_DIR"                 `# Set base directory as the current working directory  ` \
  --user $(id -u):$(id -g)       `# Use same user ID inside the container as on the host ` \
  golang:$GO_VERSION             `# Use Go's docker image with the specified tag         ` \
  go $@                          `# Run go with the provided command line arguments      `
```

Source: [learning-go/bin/go](https://github.com/fernandoacorreia/learning-go/blob/41ee9a088c12762e64814551f78ee7acf7240158/bin/go)

Essentially, this script will run Go in a Docker container, with the command-line arguments that are provided to it. For example:

```bash
bin/go run ascii-art/main.go
```

See the inline comments for details on how it works. I am sure that I will evolve this script over time as required (e.g. for cross-platform builds).

How about you? What's your preferred technique for reproducible build & run environments? And specifically for Go, do
you have any hints?
