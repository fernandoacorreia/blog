---
title: "Learning Golang: Strings" # Title of the blog post.
date: 2020-09-08T01:35:40Z # Date of post creation.
tags: ["golang"]
categories: ["learning golang"]
---

This is part 13 of my [journey](/categories/learning-golang/) learning Golang.

# Strings in Go

Strings represent a sequence of bytes. More specifically, a read-only slice of `uint8` integers.

Their main use is for representing text. This text is usually, but not necessarily, encoded as UTF-8. In Go, strings can
also be used to represent text in any encoding, and also raw bytes, not necessarily corresponding to text.

It's important to notice that strings can be empty (i.e. have a length of 0) and that they can be arbitrarily long (as
large as it will fit in memory).

# String literals

Go provides two ways for declaring string values in source code: interpreted or raw.

## Interpreted strings

The quote (`"`) character indicates an interpreted string literal. They have these characteristics:

- They can span a single line in the source file (i.e. they can't contain an unescaped newline character).
- They can contain any other character except for an unescaped double quote.
- Backslash escapes are interpreted.

Examples:

```go
"foo"                  // The word foo
"foo\nbar"             // foo, newline, and bar
"Saudações"            // UTF-8 text
"Sauda\u00E7\u00F5es"  // Unicode code points (same text as above)
```

## Raw strings

The backtick (`` ` ``) character indicates a "raw" string literal. They have these characteristics:

- They can span multiple lines in the source code.
- The raw newlines in the source file become newlines in the string constant.
- They don't interpret escape sequences.
- They can't include backticks (not even via escaping; see above).

Example:

```go
`line1
line2
line3`
```

# Declaring string variables

A string variable can be explicitly declared using the `string` type:

```go
var season string
```

And a string literal can be assigned to it like this:

```go
season = "Autumn"
```

String variables can also be declared using the `:=` shorthand notation. That will declare them with an implicit type
and assign an initial value, like this:

```go
package main

import (
  "fmt"
)

func main() {
  season := "Autumn"
  fmt.Println(season)
}
```

The code above prints:

```
Autumn
```

# String concatenation

The `+` operator will concatenate two strings. No extra spaces are added on either side.

For example:

```go
package main

import (
  "fmt"
)

func main() {
  wish := "Happy"
  season := "Autumn"
  greeting := wish + " " + season + "!"
  fmt.Println(greeting)
}
```

That creates a new string value, which is the result of the expression, and assigns it to the `greeting` variable.

The code above prints:

```
Happy Autumn!
```
