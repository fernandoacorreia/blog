---
title: "Learning Golang: Sprint, Sprintln, Sprintf" # Title of the blog post.
date: 2020-09-16T03:09:15Z # Date of post creation.
tags: ["golang"]
categories: ["learning golang"]
---

This is part 17 of my [journey](/categories/learning-golang/) learning Golang.

The `fmt` package has methods like `Print`, `Println` and `Printf` to print text to the standard output device.

It also has corresponding methods that return the strings that would be printed out, instead of actually printing them
out. Afterwards the program can use the returned values for any purpose like for instance sending an email or creating a
PDF file.

# Sprint

Returns a string containing the input arguments. No spaces or new line characters are added automatically.

For example:

```go
package main

import (
  "fmt"
)

func main() {
  quantity := 10
  fruits := "apples"
  text := fmt.Sprint("I have ", quantity, " ", fruits, ".")
  fmt.Printf("Value stored in text is: '%v'\n", text)
}
```

prints out:

```
I have 10 apples.
```

Notice that the `Printf` statement is printing out the value of the `text` variable between single quotes. The `text`
variable, in turn, contains the result of the `Sprint` statement.

Also notice how spaces were explicitly added where needed.

# Sprintln

The `Sprintln` method returns a string containing the input arguments, separated by spaces. A new line character is
added to the end of the string.

For example:

```go
package main

import (
  "fmt"
)

func main() {
  quantity := 10
  fruits := "apples"
  text := fmt.Sprintln("I have", quantity, fruits)
  fmt.Printf("Value stored in text is: '%v'\n", text)
}
```

prints out:

```
Value stored in text is: 'I have 10 apples
'
```

Compared to the `Sprint` example above, notice how it wasn't necessary to add explicit spaces, because they were added
automatically. That also made it difficult to add a trailing period without a space before it, so I removed it from the
example.

Notice how the `Printf` output is printing the value of the `text` variable between single quotes. That makes it visible
that there is a newline character at the end of the `text` string.

# Sprintf

The `Sprintf` method returns a formatted string. It interpolates a list of values according to the format specifier (the
first argument). It supports the same formatting verbs and modifiers as the [Printf](/posts/learning-golang-part-16/)
method.

For example:

```go
package main

import (
  "fmt"
)

func main() {
  quantity := 10
  fruits := "apples"
  text := fmt.Sprintf("I have %d %s.", quantity, fruits)
  fmt.Printf("Value stored in text is: '%v'\n", text)
}
```

prints out:

```
Value stored in text is: 'I have 10 apples.'
```

Notice how the first argument to `Sprintf` is the format specifier, with 2 verbs (`%d` and `%s`) as placeholders, and
how two other arguments are passed, each providing the value for one of these verbs.

Comparing `Sprintf` to the examples above, we were able to get the string formatted exactly as we wanted without needing
to add extra space arguments -- at the cost of having to learn a few simple formatting verbs.

# Takeaways

Printing out strings to console is useful, for instance for creating a basic command line interface, or for debugging
purposes.

It is often even more useful to generate a formatted string from one or more values, and to assign that to a variable.
This way the resulting string value can be used later in the program. For instance for composing the text of an email
that is going to be sent by the program, or the content of a PDF file that is going to be generated.

Of the three methods above, `Sprintf` is the most powerful and flexible. `Sprint` and `Sprintln` are simpler and can be
a good choice if all you need is concatenation.

In your experience, what are other uses for formatted strings?
