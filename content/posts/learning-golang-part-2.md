---
title: "Learning Golang: Compiling and running Go programs" # Title of the blog post.
date: 2020-08-16T01:55:20Z # Date of post creation.
categories: ["learning golang"]
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

This is part 2 of my [journey](/categories/learning-golang/) learning Golang.

# Compiling Go programs

An individual Go source file can be compiled with the `go build` command:

```
go build {filename}.go
```

That will produce an executable binary file if the source's package is `main` (see [Part 3](/posts/learning-golang-part-3/) for more on packages).

The resulting binary can be executed with this command:

```
./{filename}
```

Example:

```
$ go build main.go
$ ./main
Hello World
```

# Running from source

The `go run` command combines the two previous steps: it builds a binary from a source file and executes it:

```
go run {filename}.go
```

That's super handy for an interactive workflow during development.

Example:

```
$ go run main.go
Hello World
```

`go run` does **not** create a binary in the current folder.

# Takeaways

- `go build` will compile and produce a binary.
- `go run` will compile and run without producing a binary.

This looks like a pretty handy workflow to me. What do you think? How does that compare to your experience with other
languages? If you're a seasoned Go programmer, what would you add to these notes?
