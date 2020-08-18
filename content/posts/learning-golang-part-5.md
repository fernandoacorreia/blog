---
title: "Learning Golang: Comments" # Title of the blog post.
date: 2020-08-18T04:02:00Z # Date of post creation.
tags: ["golang"]
categories: ["learning golang"]
codeMaxLines: 20 # Override global value for how many lines within a code block before auto-collapsing.
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

This is part 5 of my [journey](/categories/learning-golang/) learning Golang.

# Inline comments

Go ignores text to the right of `//`:

```go
// This entire line is ignored by the compiler.
// fmt.Println("Does NOT print")
fmt.Println("This gets printed!") // This part gets ignored
```

# Block comments

All lines between `/*` and `*/` will be ignored:

```go
/*
This is ignored.
This is also ignored.
fmt.Println("This WON'T print!")
*/
```

# Godoc

Go has a tool for automatically generating documentation from Go source code: [Godoc](https://godoc.org/golang.org/x/tools/cmd/godoc).

From the [blog post](https://blog.golang.org/godoc) that announced it in 2011:

> Godoc parses Go source code - including comments - and produces documentation as HTML or plain text.

See an example in HTML format: [zip - GoDoc](https://godoc.org/archive/zip).

Godoc follows some simple [conventions](https://github.com/golang/go/wiki/Comments).

# Package comments

This type of comment should be present in one of the source files of a package:

```go
// Package sort provides primitives for sorting slices and user-defined
// collections.
package sort
```

# Top-level identifier comments

This is the format for describing a top-level function, `const`, `var`, etc.:

```go
// enterOrbit causes Superman to fly into low Earth orbit, a position
// that presents several possibilities for planet salvation.
func enterOrbit() os.Error {
  ...
}
```

# Code samples in comments

Indented text inside of a comment will be rendered as a pre-formatted block by Godoc:

```go
// fight can be used on any enemy and returns whether Superman won.
//
// Examples:
//
//  fight("a random potato")
//  fight(LexLuthor{})
//
func fight(enemy interface{}) bool {
  ...
}
```

# Bug comments

Godoc ignores most comments that are not right above a top-level element. A bug comment is an exception: it will be
included in the package's documentation under a "Bugs" section:

```go
// BUG(name): The rule Title uses for word boundaries does not handle Unicode punctuation properly.
```

The text in the parenthesis block is the user name of someone that can provide more information about the bug.

# Deprecation notes

Elements that became redundant or obsolete can be marked with a paragraph in their doc comments that begins with
"Deprecated:" followed by some information about the deprecation:

```go
// ModTime returns the modification time in UTC using the legacy
// ModifiedDate and ModifiedTime fields.
//
// Deprecated: Use Modified instead.
func (h *FileHeader) ModTime() time.Time {
  return msDosTimeToTime(h.ModifiedDate, h.ModifiedTime)
}
```
