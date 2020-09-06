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

# Variables

A variable is a named value that can change during the execution of a program. I.e. a variable's value can be updated at
run time.

## Variable declarations

In Go, variables are declared following this pattern: `var` {identifier} {type}. Examples:

```go
var songName string
var lengthOfSong uint16
var isMusicOver bool
var songRating float32
```

## Zero values

If a value is not assigned to the variable when it is declared (like above) then it is initialized with a "zero value".
The actual value depends on the data type. Generally:

- 0 for numeric data types
- false for the boolean data type
- empty string for string data type

## Default values

The initial value of a variable can be assigned when it is declared:

```go
var shoppingCartQuantity = 1
var shoppingCartItemName = "cupholder"
var shoppingCartPrice = 19.99
var shoppingCartExtendedWarranty = true
```

# Arithmetic

We can perform arithmetic in Go with literals (or named values, covered in the next exercise) using the following operators:

- `+` to add
- `-` to subtract
- `*` to multiply
- `/` to divide
- `%` to take the remainder (the modulus operator) between two numbers.
