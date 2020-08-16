---
title: "Learning Golang: Packages" # Title of the blog post.
date: 2020-08-16T02:12:03Z # Date of post creation.
categories: ["learning golang"]
tags: ["Untagged"]
codeLineNumbers: true
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

This is part 3 of my [journey](/categories/learning-golang/) learning Golang.

# Package declaration

The first line of a Go source file is the "package declaration", defined by the `package` keyword.

This serves a few purposes:
- It provides a structure for grouping related source files.
- It provides a mechanism for code reuse.
- It differentiates between executable packages from utility packages (i.e. libraries).

Example:

```go
package main
```

`go build` will produce an executable binary file for source files with `package main`.

# Importing packages

The `import` keyword allows bringing in and using code from other packages.

Example:

```go
import "fmt"
```

A "package reference variable" is created from the imported package's name -- in this case, `fmt`.

# Full example

This is a full "Hello World" example in Go that demonstrates the concepts above.

Notice that the first line is a package declaration with a package name of `main`. That will make this an executable
program.

On line 3, the `fmt` package is being imported, so that its `Println` function can be used on line 6.

```go
package main

import "fmt"

func main () {
  fmt.Println("Hello World")
}
```

# Takeaways

- The `package` keyword is used for the obligatory package declaration.
- The `import` keyword is used for bringing into context code from other packages.
- `main` is a special package name for executable programs.

If you know Go, what would you add to an initial exposure on the concept of packages?
