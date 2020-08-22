---
title: "Learning Golang: Running Go in a container" # Title of the blog post.
date: 2020-08-22T01:55:41Z # Date of post creation.
tags: ["golang"]
categories: ["learning golang"]
draft: true # Sets whether to render this page. Draft of true will not be rendered.
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


# Running Go from a Docker container

Error:

```
❯ bin/go run gopher/main.go
failed to initialize build cache at /.cache/go-build: mkdir /.cache: permission denied
```
