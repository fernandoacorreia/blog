---
title: "Learning Golang: Scan, Scanln and Scanf" # Title of the blog post.
date: 2020-09-19T16:09:07Z # Date of post creation.
tags: ["golang"]
categories: ["learning golang"]
---

This is part 18 of my [journey](/categories/learning-golang/) learning Golang.

# Command line interface

When building programs that run on a terminal it is often useful to be able to allow the user to enter text.

For instance the `ssh-keygen` utility will prompt for a path and a passphrase.

```
❯ ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
Generating public/private rsa key pair.
Enter file in which to save the key (/home/fernando/.ssh/id_rsa): /tmp/test_rsa
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
```

# Scan

The `Scan` method of the `fmt` package will read a single space-separated token (like a single word) from the standard
input device (which is usually the console).

`Scan` expects an address as its argument. That can be provided by using the `&` symbol in front of a variable name.

For example:

```go
package main

import (
  "fmt"
)

func main() {
  fmt.Print("What is your first name? ")
  var response string
  fmt.Scan(&response)
  fmt.Printf("Hello, %v!\n", response)
}
```

Source: [learning-go/scanning/scan.go](https://github.com/fernandoacorreia/learning-go/blob/624ebfb008efbb446abccace077df08f5ffe9c3b/scanning/scan.go)


This program, when executed, will wait for the user to enter a line of text, and then it will take the first word of
that line (until it finds a space or the end of the line):

```
❯ go run ./scanning/scan.go
What is your first name? Jane
Hello, Jane!
```

If more than one word is entered, only the first one is read by `Scan`. The remainder is left in the console and can be
read by another `Scan` call. For example:

```
❯ go run ./scanning/scan.go
What is your first name? Jane Doe
Hello, Jane!

❯ Doe
zsh: Doe: command not found...
```

Notice how the rest of the input was left in the console, and was read by the terminal after the program finished.

# Scanln

The `Scanln` method is similar to `Scan`. It will also read space-separated tokens. Two differences are:

- it will stop at a newline character;
- it requires a newline or EOF character after the last item.

# Scanf

According to the [documentation](https://golang.org/pkg/fmt/#Scanf):

> Scanf scans text read from standard input, storing successive space-separated values into successive arguments as determined by the format. It returns the number of items successfully scanned. If that is less than the number of arguments, err will report why. Newlines in the input must match newlines in the format. The one exception: the verb %c always scans the next rune in the input, even if it is a space (or tab etc.) or newline.

`Scanf` adds finer-grained control (via a format string) to input parsing.

# Reading full lines from the console

If the program requires reading a full line from standard input, instead of using the `fmt` package it is better to use
the `bufio` package.

This article teaches how to do that: [Reading in Console Input in Golang](https://tutorialedge.net/golang/reading-console-input-golang/).

# Takeaways

The "Scan" family of methods in the `fmt` package is meant for reading tokens and other kinds of delimited values from
standard input.

The `bufio` package is better suited for interacting with users via a command line interface.
