---
title: "Learning Golang: Multiline strings" # Title of the blog post.
date: 2020-08-21T03:18:04Z # Date of post creation.
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

This is part 7 of my [journey](/categories/learning-golang/) learning Golang.

My first assignment on Codecademy's [Learn Go](https://www.codecademy.com/learn/learn-go) course was to create a program
that prints out [ASCII art](https://www.asciiart.eu/computers/computers).

The way that's different from a "Hello, World" program is that it needs to print multiple lines. So it was a great
opportunity to learn about how multi-line strings can be represented in Go.

# Go's string literals

String literals represent "string constants" i.e. immutable string values in a Go source file.

There are two ways of declaring [string literals](https://golang.org/ref/spec#String_literals) in Go: using quotes and using backticks. The first one declares an "interpreted string", and the second one a "raw string". There are also "rune literals", which are not properly strings, but represent a single character.

# Interpreted strings

A string literal declared between double quotes (`"`) is an interpreted string.

The characteristics of interpreted strings are:
- They can span a single line in the source file.
- They can contain any character except for a "raw" newline or an unescaped double quote.
- Backslash escapes are interpreted.

Examples:

```go
"foo"                  // The word foo
"foo\nbar"             // foo, newline, and bar
"Saudações"            // UTF-8 text
"Sauda\u00E7\u00F5es"  // Unicode code points (same text as above)
```

# Raw strings

A string literal declared between backticks (AKA "back quotes") is a raw string. It has these characteristics:

- It can span multiple lines in the source code.
- The raw newlines in the source file become newlines in the string constant.
- It doesn't interpret escape sequences.
- It can't include backticks (not even via escaping; see above).

# Rune literals

Quoting Go's [documentation](https://golang.org/ref/spec#Rune_literals), "a rune literal represents a rune constant, an integer value identifying a Unicode code
point." Conceptually it represents a single character (keeping in mind that it's Unicode).

Run literals also interpret backslash escapes.

Examples:

```go
'a'
'ã'
'\t'
'\377'
'\xff'
'\u12e4'
'\U00101234'
```

# ASCII art in Go source code

The [ASCII art](http://www.ascii-fr.com/-Computers-.html) that I wanted to print from my first Go program made liberal use of all sorts of symbols like backticks
(\`), single quotes (') and backslashes (\\). It also had multiple lines, of course.

I had a few alternatives for representing it in a source file:

1. Between double quotes: I'd need to break it down into multiple string constants (one per line) and escape the
   backslash and double quote characters. It would work, but it would look distorted in the source file.
2. A very long, single-line interpreted script, with escaped newline characters. That's unwieldy.
3. Between backticks: I'd have a single multi-line string, and I wouldn't need to escape anything. But I wouldn't be
   able to use backticks in the string itself.

Another alternative of course would be to not embed the string in a Go source file, but that is outside the goal of the exercise.
In fact this exercise was quite clever because it forced me to learn a lot about string literals in Go.

I decided to go with option 3 -- backticks -- mainly because the embedded string looks better in a Go source file if it
isn't escaped. I compromised by replacing the backtick characters with backslashes in the ASCII art.

This was my end result:

```go
package main

import (
  "fmt"
)

func main() {
  // Credit: unknown artist.
  fmt.Println(`    888888888888888888888
  s 88 ooooooooooooooo 88     s 888888888888888888888888888888888888888
  S 88 888888888888888 88    SS 888888888888888888888888888888888888888
 SS 88 888888888888888 88   SSS 8888                         - --+ 8888
 SS 88 ooooooooooooooo 88  sSSS 8888           o8888888o         | 8888
sSS 88 888888888888888 88 SSSSS 8888         o88888888888o         8888
SSS 88 888888888888888 88 SSSSS 8888        8888 88888 8888      | 8888
SSS 88 ooooooooooooooo 88 SSSSS 8888       o888   888   888o       8888
SSS 88 888888888888888 88 SSSSS 8888       8888   888   8888       8888
SSS 88 888888888888888 88 SSSSS 8888       8888   888   8888       8888
SSS 88 oooooooooo      88 SSSSS 8888       8888o o888o o8888       8888
SSS 88 8888888888 .::. 88 SSSSS 8888       988 8o88888o8 88P       8888
SSS 88 oooooooooo :::: 88 SSSSS 8888        8oo 9888889 oo8        8888
SSS 88 8888888888  \'  88 SSSSS 8888         988o     o88P         8888
SSS 88ooooooooooooooooo88  SSSS 8888           98888888P           8888
SSS 888888888888888888888__SSSS 8888                               8888_____
SSS |   *  *  *   )8c8888  SSSS 888888888888888888888888888888888888888
SSS 888888888888888888888.  SSS 888888888888888888888888888888888888888
SSS 888888888888888888888 \_ SSsssss oooooooooooooooooooooooooooo ssss
SSS 888888888888888888888  \\   __SS 88+-8+-88============8-8==88 S
SSS 888888888888888888888-. \\  \  S 8888888888888888888888888888
SSS 888888888888888888888  \\\  \\       \.__________.'      \ .
SSS 88O8O8O8O8O8O8O8O8O88  \\.   \\______________________________\_.
SSS 88 el cheapo 8O8O8O88 \\  '.  \|________________________________|
 SS 88O8O8O8O8o8O8O8O8O88  \\   '-.___
  S 888888888888888888888 /~          ~~~~~-----~~~~---.__
 .---------------------------------------------------.    ~--.
 \ \______\ __________________________________________\-------^.-----------.
 :'  _   _ _ _ _  _ _ _ _  _ _ _ _   _ _ _           \\        \
 ::\ ,\_\,\_\_\_\_\\_\_\_\_\\_\_\_\_\,\_\_\_\           \      o '8o 8o .
 |::\  -_-_-_-_-_-_-_-_-_-_-_-_-_-___  -_-_-_   _ _ _ _  \      8o 88 88 \
 |_::\ ,\_\_\_\_\_\_\_\_\_\_\_\_\_\___\,\_\_\_\,\_\_\_\_\ \      88       \
    \:\ ,\__\_\_\_\_\_\_\_\_\_\_\_\_\  \,\_\_\_\,\_\_\_\ \ \      88       .
     \:\ ,\__\_\_\_\_\_\_\_\_\_\_\_\____\    _   ,\_\_\_\_\ \      88o    .|
       :\ ,\____\_\_\_\_\_\_\_\_\_\_\____\  ,\_\ _,\_\_\_\ \ \      'ooooo'
        :\ ,\__\\__\_______________\__\\__\,\_\_\_\,\___\_\_\ \
         \\  --  -- --------------- --  --   - - -   --- - -   )____________
           \--------------------------------------------------'
`)
}
```
Source: [ascii-art/main.go](https://github.com/fernandoacorreia/learning-go/blob/7c489be6bb0b6625c1f6a8e46f2ae56dfc363035/ascii-art/main.go)

# Takeaways

Go offers 3 ways to represent string or character literals:

| Syntax              | Symbol              | Span                  | Escaping |
| :-----------------: | :-----------------: | :-------------------: | -------: |
| Interpreted strings | double quotes (`"`) | Single source line    | Yes      |
| Raw strings         | backticks (`` ` ``) | Multiple source lines | No       |
| Rune literals       | single quotes (`'`) | Single code point     | Yes      |

What else would you point out about strings in Go?
