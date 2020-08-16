---
title: "Learning Golang: Function declarations" # Title of the blog post.
date: 2020-08-16T17:31:12Z # Date of post creation.
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

This is part 4 of my [journey](/categories/learning-golang/) learning Golang.

# Function declarations

Functions are reusable blocks of code. For example:

```go
func main () {
    fmt.Println("Hello, World!")
}
```

The `func` keyword declares a function. It is followed by the function's name, a list of arguments (delimited by
parenthesis) and the function block (delimited by curly braces).

# main function

In Go, the `main` function is special. When the `main` function is defined in the `main` package, it is automatically
called when the program is executed.
