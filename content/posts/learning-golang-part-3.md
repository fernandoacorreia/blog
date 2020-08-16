---
title: "Learning Golang: Packages" # Title of the blog post.
date: 2020-08-16T02:12:03Z # Date of post creation.
tags: ["golang"]
categories: ["learning golang"]
codeLineNumbers: true
codeMaxLines: 20 # Override global value for how many lines within a code block before auto-collapsing.
# description: "Article description." # Description used for search engine.
# featured: true # Sets if post is a featured post, making appear on the home page side bar.
# toc: false # Controls if a table of contents should be generated for first-level links automatically.
# menu: main
# featureImage: "/images/path/file.jpg" # Sets featured image on blog post.
# thumbnail: "/images/path/thumbnail.png" # Sets thumbnail image appearing inside card on homepage.
# shareImage: "/images/path/share.png" # Designate a separate image for social media sharing.
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

# Importing a package

The `import` keyword allows bringing in and using code from other packages.

Example:

```go
import "fmt"
```

A "package reference variable" is created from the imported package's name -- in this case, `fmt`.

# Importing multiple packages

It's usual for a source file to import multiple packages. The convention for that is to use a single `import` statement
with a package list within parenthesis like this:

```go
import (
  "package1"
  "package2"
)
```

# Package alias

It is possible to define an "alias" as a shorthand name instead of the default package reference variable. The syntax
for that is to specify the alias before the package name like this:

```go
import (
  p1 "package1"
  "package2"
)
```

That allows calling functions in `package1` like this:

```go
p1.SampleFunc()
```

# Full example

This is a full "Hello World" example in Go that demonstrates the concepts above.

```go
package main

import (
  "fmt"
  t "time"
)

func main() {
  fmt.Println("Hello, World!")
  fmt.Println("The time is now ", t.Now())
}
```

Highlights:
- Line 1: The package declaration with a package name of `main`. That will make this an executable program.
- Line 3: The `import` statement is importing a list of packages.
- Line 4: Imports the "fmt" package with its standard name ("fmt").
- Line 5: Imports the "time" package with the alias "t".
- Line 9: Uses the `Println` function from package `fmt` to display "Hello, World!"
- Line 10: Uses the `Println` function from package `fmt` to display "The time is now " followed by the current time, as
  returned by function `Now` from package `time` (aliased as `t`).

This is a sample output of the program above:

```
$ go run main.go
Hello, World!
The time is now  2020-08-16 18:07:24.180778888 +0000 UTC m=+0.000097040
```

# Takeaways

- The `package` keyword is used for the obligatory package declaration.
- The `import` keyword is used for bringing into context code from other packages.
- `main` is a special package name for executable programs.

If you know Go, what would you add to an initial exposure on the concept of packages?
