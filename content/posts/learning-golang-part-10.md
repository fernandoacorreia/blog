---
title: "Learning Golang: Literals and Constants" # Title of the blog post.
date: 2020-09-06T17:55:33Z # Date of post creation.
tags: ["golang"]
categories: ["learning golang"]
---

This is part 10 of my [journey](/categories/learning-golang/) learning Golang.

# Literals

In Go, values can be many things. Just to name a few, values can be numbers (like 109), or text wrapped in quotes (like "Hello world").

Literals are values written in the source code. For example:

```go
fmt.Println("Hello, world!")       // String literal
fmt.Println(42)                    // Integer literal
fmt.Println(3.141592653589793238)  // Floating point literal
```

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
