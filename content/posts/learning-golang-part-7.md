---
title: "Learning Golang: My first Go program" # Title of the blog post.
date: 2020-08-21T03:18:04Z # Date of post creation.
tags: ["Untagged"]
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

**Insert Lead paragraph here.**

# Multiline strings

- backtick
- can't include other backticks
- does not interpret escapes or unicode characters
- double quotes does not allow multiline
- single quotes is for characters

# Running Go from a Docker container

Error:

```
❯ bin/go run gopher/main.go
failed to initialize build cache at /.cache/go-build: mkdir /.cache: permission denied
```
