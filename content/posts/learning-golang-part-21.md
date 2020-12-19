---
title: "Learning Golang: switch" # Title of the blog post.
date: 2020-12-19T18:59:21Z # Date of post creation.
tags: ["golang"]
categories: ["learning golang"]
---

This is part 21 of my [journey](/categories/learning-golang/) learning Golang.

# Chained conditions

It is a common pattern for a program to have a sequence of conditional statements testing for different values of the
same variable or function result.

For instance:

```go
package main

import (
  "fmt"
)

func main() {
  x := 0
  y := 0
  for command := ""; command != "end"; {
    fmt.Print("Command? ")
    fmt.Scan(&command)
    if command == "up" {
      y -= 1
    } else if command == "down" {
      y += 1
    } else if command == "left" {
      x -= 1
    } else if command == "right" {
      x += 1
    } else if command == "end" {
      fmt.Println("Exiting.")
    } else {
      fmt.Printf("Invalid command: %v\n", command)
    }
    fmt.Printf("x=%v, y=%v\n", x, y)
  }
}
```

Source: [learning-go/switch/if-else.go](https://github.com/fernandoacorreia/learning-go/blob/1f6a68a8a72624870a1839ec022785c1c272284a/switch/if-else.go)

This program produces an output like this:

```
❯ bin/go run ./switch/if-else.go
Command? right
x=1, y=0
Command? down
x=1, y=1
Command? right
x=2, y=1
Command? up
x=2, y=0
Command? left
x=1, y=0
Command? back
Invalid command: back
x=1, y=0
Command? end
Exiting.
x=1, y=0
```

Notice the chained `if` statements testing for different values of `command`.

The `switch` statement can be used to simplify code like this and to make the pattern more evident.

# switch

The `switch` statement will execute the statements in the first `case` expression that matches the value of its operand.

For example:

```go

package main

import (
  "fmt"
)

func main() {
  x := 0
  y := 0
  for command := ""; command != "end"; {
    fmt.Print("Command? ")
    fmt.Scan(&command)
    switch command {
    case "up":
      y -= 1
    case "down":
      y += 1
    case "left":
      x -= 1
    case "right":
      x += 1
    case "end":
      fmt.Println("Exiting.")
    default:
      fmt.Printf("Invalid command: %v\n", command)
    }
    fmt.Printf("x=%v, y=%v\n", x, y)
  }
}
```

Source: [learning-go/switch/switch.go](https://github.com/fernandoacorreia/learning-go/blob/71cfbfcb88715980668712fea19c91aa7e4d4ce9/switch/switch.go)

This program produces an output like this:

```
❯ bin/go run ./switch/switch.go
Command? right
x=1, y=0
Command? down
x=1, y=1
Command? right
x=2, y=1
Command? up
x=2, y=0
Command? left
x=1, y=0
Command? back
Invalid command: back
x=1, y=0
Command? end
Exiting.
x=1, y=0
```

Notice how each `case` expression checks for a different value of the same variable (`command`).

The statements in the `default` case will be executed if none of the `case` expressions matched.

# Variable case conditions

The value in a `case` expression does not need to be a constant literal. It can be a variable, or the return value of a
function call.

For example:

```go
package main

import (
  "fmt"
)

func main() {
  x := 0
  y := 0
  endCommand := "end"
  for command := ""; command != endCommand; {
    fmt.Print("Command? ")
    fmt.Scan(&command)
    switch command {
    case "up":
      y -= 1
    case "down":
      y += 1
    case "left":
      x -= 1
    case "right":
      x += 1
    case endCommand:
      fmt.Println("Exiting.")
    default:
      fmt.Printf("Invalid command: %v\n", command)
    }
    fmt.Printf("x=%v, y=%v\n", x, y)
  }
}
```

Source: [learning-go/switch/switch.go](https://github.com/fernandoacorreia/learning-go/blob/f9cdde1754baf7234ef77868b7cc66e4c3317757/switch/switch.go)

This program produces an output like this:

```
❯ bin/go run ./switch/switch.go
Command? end
Exiting.
x=0, y=0
```

Notice how instead of checking for the literal `"end"`, the program checks for the value of the `endCommand` variable.

# Summary

The `switch` statement improves code readability when there is a chain of conditional statements that test for different
values of the same variable or function result.

The statements of the first matching `case` expression will be executed. If no `case` expression matches, the `default`
statements will be executed, if they are present.
