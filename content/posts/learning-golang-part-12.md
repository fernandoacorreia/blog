---
title: "Learning Golang: Compilation Errors" # Title of the blog post.
date: 2020-09-07T21:06:17Z # Date of post creation.
tags: ["golang"]
categories: ["learning golang"]
---

This is part 12 of my [journey](/categories/learning-golang/) learning Golang.

# Compile-time errors

Go is a compiled language. That means that it will parse the source code and produce an executable binary file from it.

The compiler parses the code according to strictly defined rules. That allows Go programs to run more efficiently than
if they were interpreted as they run.

As a valuable side-effect, it will reveal many kinds of errors (like typos or invalid code) immediately when the
programs are compiled, as opposed to only when that particular part of the program is executed.

In order to maximize the value from this early verification, Go is more strict than most languages and will not compile
code with abnormalies that would be ignored by other languages. For instance, it will produce an error if a variable is
declared but never used. At best, that is dead code that may indicate a subtler problem (like a missing statement). It
can also have been a typo. Either way, Go will tell you about the problem so that you can fix it before proceeding.

# Structure of compiler error messages

When the Go compiler is asked to compile invalid code, it will print out an error message.

The compiler's error message will include:
- the name of the file where the error was detected;
- the line number in that file where the error is present;
- the column on that line in which the error occurred.

For example, compiling this program:

```go
package main

func main() {
  fmt.Println("Hello, world!")
}
```

will produce this error:

```
./main.go:4:3: undefined: fmt
```

Where "main.go" is the file name, 4 is the line number, and 3 is the column number.

That message is indicating that the `fmt` identifier us not defined. That can be fixed by adding an `import "fmt"` line
after the "package" statement.

# Takeaways

Go performs a strict check for syntax errors, invalid code and other abnormalies when compiling a source file.

If it finds a problem, it will print out an error message and it won't produce an executable binary.

What is your experience with compilation errors in Go? How would you compare it to other languages?
