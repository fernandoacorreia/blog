---
title: "Learning Golang: Logical operators" # Title of the blog post.
date: 2020-10-09T03:32:37Z # Date of post creation.
tags: ["golang"]
categories: ["learning golang"]
---

This is part 20 of my [journey](/categories/learning-golang/) learning Golang.

# Boolean algebra

Boolean algebra is about logical operations applied to the boolean values `true` and `false`.

The most common operations are "and" (conjunction), "or" (disjunction) and "not" (negation).

Fun fact: it is called "boolean" because it was introduced by George Boole in 1847.

# Logical operators

Go provides three operators for boolean algebra, called "logical operators":

- `&&`: AND operator.
- `||`: OR operator.
- `!`: NOT operator.

## And

The `&&` operator takes two boolean values and it produces `true` if and only if **both** its operands are `true`.

In other words: `p && q` is "if p then q else false".

In table format:

|           | true     | false    |
| :-------  | :------- | :------- |
| **true**  | true     | false    |
| **false** | false    | false    |

Example:

```go
package main

import (
  "os"
  "bufio"
  "fmt"
  "strings"
)

func main() {
  reader := bufio.NewReader(os.Stdin)

  fmt.Print("Are the lights on (y/n)? ")
  lightsOnInput, _ := reader.ReadString('\n')
  lightsOnCleaned := strings.TrimSuffix(lightsOnInput, "\n")
  lightsOn := lightsOnCleaned == "y"

  fmt.Print("Is the door open (y/n)? ")
  doorOpenInput, _ := reader.ReadString('\n')
  doorOpenCleaned := strings.TrimSuffix(doorOpenInput, "\n")
  doorOpen := doorOpenCleaned == "y"

  if lightsOn && doorOpen {
    fmt.Println("Go in.")
  } else {
    fmt.Println("Come back later.")
  }
}
```

Source:
[learning-go/logical/and.go](https://github.com/fernandoacorreia/learning-go/blob/cab6ed1c278aa69f87deb2371ddd9d66ba6ddc50/logical/and.go)

Sample runs:

```
❯ bin/go run ./logical/and.go
Are the lights on (y/n)? y
Is the door open (y/n)? y
Go in.

❯ bin/go run ./logical/and.go
Are the lights on (y/n)? n
Is the door open (y/n)? y
Come back later.

❯ bin/go run ./logical/and.go
Are the lights on (y/n)? y
Is the door open (y/n)? n
Come back later.
```

## Or

The `||` operator takes two boolean values and it produces `true` if **either** of its operands is `true` (or if both are
`true`).

In other words: `p || q` is "if p then true else q".

In table format:

|           | true       | false       |
| :-------  | :-------   | :-------    |
| **true**  | true       | true        |
| **false** | true       | false       |

Example:

```go
package main

import (
  "bufio"
  "fmt"
  "os"
  "strings"
)

func main() {
  reader := bufio.NewReader(os.Stdin)

  fmt.Print("What day of the week is it? ")
  dowInput, _ := reader.ReadString('\n')
  dow := strings.TrimSuffix(dowInput, "\n")

  if dow == "Saturday" || dow == "Sunday" {
    fmt.Println("Stay home.")
  } else {
    fmt.Println("Go to work.")
  }
}
```

Source:
[learning-go/logical/or.go](https://github.com/fernandoacorreia/learning-go/blob/cab6ed1c278aa69f87deb2371ddd9d66ba6ddc50/logical/or.go)

Sample runs:

```
❯ bin/go run ./logical/or.go
What day of the week is it? Saturday
Stay home.

❯ bin/go run ./logical/or.go
What day of the week is it? Sunday
Stay home.

❯ bin/go run ./logical/or.go
What day of the week is it? Monday
Go to work.
```

## Not

The `!` operator returns `true` if its operand is `false` and `false` if its operand is `true`. It reverses ("negates")
the value of its operand.

In other words: `!p` is "not p".

In table format:

|           | !        |
| :-------  | :------- |
| **true**  | false    |
| **false** | true     |

Example:

```go
package main

import (
  "bufio"
  "fmt"
  "os"
  "strings"
)

func main() {
  reader := bufio.NewReader(os.Stdin)

  fmt.Print("Are you hungry (y/n)? ")
  hungryInput, _ := reader.ReadString('\n')
  hungryCleaned := strings.TrimSuffix(hungryInput, "\n")
  hungry := hungryCleaned == "y"
  notHungry := !hungry

  fmt.Println("You are hungry:", hungry)
  fmt.Println("You are satisfied:", notHungry)
}
```

Source:
[learning-go/logical/not.go](https://github.com/fernandoacorreia/learning-go/blob/cab6ed1c278aa69f87deb2371ddd9d66ba6ddc50/logical/not.go)

Sample runs:

```
❯ bin/go run ./logical/not.go
Are you hungry (y/n)? y
You are hungry: true
You are satisfied: false

❯ bin/go run ./logical/not.go
Are you hungry (y/n)? n
You are hungry: false
You are satisfied: true
```

# Takeaways

- Go has three operators for boolean arithmetic: `&&` (and), `||` (or) and `!` (not).
- These operators are very useful for writing conditions for `if` statements.
- They're also useful whenever a boolean value needs to be produced based on one or more boolean values.
- Relational operators (such as `==`, `<`, `>`, etc.) return boolean values and are easy to use in boolean expressions.
