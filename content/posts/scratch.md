---
title: "Scratch" # Title of the blog post.
date: 2020-08-26T03:12:32Z # Date of post creation.
tags: ["Untagged"]
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

# Values

In Go, values can be many things. Just to name a few, values can be numbers (like 109), or text wrapped in quotes (like "Hello world").

# Literals

Literals are values written in the source code.

# Constants

In addition to literal values (i.e. values directly expressed in the source code), Go also allows "named values", i.e.
values identified by a name. These named values are called "constants" because the value represented by the name remains
the same throughout the runtime of the program.

Example:

```go
package main

import (
  "fmt"
)

func main() {
  const inchesPerFeet = 12
  fmt.Println("There are", inchesPerFeet, "inches in a foot.")
}
```

This program prints `There are 12 inches in a foot.`

# Variables

# Arithmetic

We can perform arithmetic in Go with literals (or named values, covered in the next exercise) using the following operators:

- `+` to add
- `-` to subtract
- `*` to multiply
- `/` to divide
- `%` to take the remainder (the modulus operator) between two numbers.
