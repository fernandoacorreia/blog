---
title: "Learning Golang: Values and Variables" # Title of the blog post.
date: 2020-08-24T00:45:00Z # Date of post creation.
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

This is part 9 of my [journey](/categories/learning-golang/) learning Golang.

# Data types

Data types are a designation by a programming language about the kind of values that are being stored.

Go has several basic data types built in.

## Integer numbers

These represent whole numbers.

| Data type | Number of bits | Minimum value              | Maximum value              |
| :-------- | -------------: | -------------------------: | -------------------------: |
| bool      | 1              | 0 (false)                  | 1 (true)                   |
| int8      | 8              | -128                       | 127                        |
| int16     | 16             | -32,768                    | 32,767                     |
| int32     | 32             | -2,147,483,648             | 2,147,483,647              |
| int64     | 64             | -9,223,372,036,854,775,808 | 9,223,372,036,854,775,807  |
| uint8     | 8              | 0                          | 255                        |
| uint16    | 16             | 0                          | 65,535                     |
| uint32    | 32             | 0                          | 4,294,967,295              |
| uint64    | 64             | 0                          | 18,446,744,073,709,551,615 |

## Floating-point numbers

These represent numbers that may have a fractional part.

| Default Header | Left Align | Right Align | Center Align |
| --- | :-- | --: | :-: |
| x | x | x | x |


## Complex numbers

These represent numbers with an imaginary component. They're useful for computations on 2-dimensional space and
calculations involving square roots.

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

# Takeaways

