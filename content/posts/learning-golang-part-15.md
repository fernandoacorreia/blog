---
title: "Learning Golang: Println and Print" # Title of the blog post.
date: 2020-09-12T04:21:49Z # Date of post creation.
tags: ["golang"]
categories: ["learning golang"]
---

This is part 15 of my [journey](/categories/learning-golang/) learning Golang.

# fmt Package

Go's fmt package implements formatted I/O with formatting functions in the venerable, old-school style of the C
language, but modernized.

This article covers the most basic functions for printing out text `Println` and `Print`:

# Println

The `Println` function prints outs a line of text to the standard output device.

It prints its arguments, with a space between them, and a new line character at the end.

For example, this program:

```go
package main

import "fmt"

func main() {
  fmt.Println("Line", 1)
  fmt.Println("This", "is", "line", 2)
  fmt.Println("End")
}
```

prints out:

```
Line 1
This is line 2
End
```

# Print

The `Print` function prints out its arguments without adding spaces in between. It also doesn't add a new line
character.

For instance this program:

```go
package main

import "fmt"

func main() {
  points := 25750
  rating := "HIGH SCORE!"
  fmt.Print("Your points", ": ")
  fmt.Print(points)
  fmt.Print(" (", rating, ")")
}
```

prints out:

```
Your points: 25750 (HIGH SCORE!)
```

Notice how the spaces are embedded in the arguments. Also, a line break was not added at the end. The next output would
continue on the same line.

