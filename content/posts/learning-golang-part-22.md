---
title: "Learning Golang: Scoped shorthand variable declaration" # Title of the blog post.
date: 2021-02-14T03:24:01Z
tags: ["golang"]
categories: ["learning golang"]
---

This is part 22 of my [journey](/categories/learning-golang/) learning Golang.

# Variable scopes

A common source of errors in programming is using the same variable in many different parts of a program. For a deep
dive into the problems that this practice can cause, take a look at [Global Variables Are
Bad](https://wiki.c2.com/?GlobalVariablesAreBad).

A common solution that is adopted by most programming languages is to make it possible to declare variables that can
only be used by a subset of the program. For instance, by a single module, class, function, or statement inside of a
function. This concept of the area of a program that can use a given identifier is called a "scope". The smaller the
scope, the smaller the amount of logic that can deal with that variable, and the smaller the chance of subtle errors
creeping in.

# Declaring a variable in the scope of a statement

Go has a shorthand notation for declaring a variable that is only "visible", i.e. can only be used in the code that
belongs to a single statement.

That can be done by assigning a value to a variable immediately after the statement keyword, and by continuing the
stament after a semi-colon (`;`) character. See the examples below:

## if

A variable can be declared (and initialized) before the condition of an `if` statement is provided, like this:

```go
value := 1
limit := 0
if variable := value; variable > limit {
  fmt.Println(variable)
}
```

The identifier (in this case, `variable`) only exists in the scope of the `if` statement.

See how this can be used in a program:

```go
package main

import (
  "bufio"
  "fmt"
  "os"
  "strconv"
  "strings"
)

func main() {
  maxPurchase := 1000.0
  quantity := readNumber("Quantity")
  unitPrice := readNumber("Unit price")
  taxes := readNumber("Taxes")
  if total := quantity * unitPrice * (1 + taxes); total > maxPurchase {
    fmt.Printf("Purchase denied: $%.2f is above $%.2f.\n", total, maxPurchase)
  } else {
    fmt.Printf("Purchase approved: $%.2f\n", total)
  }
}

func readNumber(label string) float64 {
  fmt.Print(label + "? ")
  reader := bufio.NewReader(os.Stdin)
  rawInput, _ := reader.ReadString('\n')
  input := strings.TrimSuffix(rawInput, "\n")
  if result, err := strconv.ParseFloat(input, 64); err == nil {
    return result
  }
  panic("Invalid input.")
}
```

Source: [learning-go/shorthand-scoped-var/if.go](https://github.com/fernandoacorreia/learning-go/blob/950efb2813e410cda0c6a1c335e5f78525f52102/shorthand-scoped-var/if.go)

When executed, it produces an output like this:

```
Quantity? 2
Unit price? 12.99
Taxes? 0.05
Purchase approved: $27.28
```

or like this:

```
Quantity? 100
Unit price? 19.99
Taxes? 0.12
Purchase denied: $2238.88 is above $1000.00.
```

Notice that this program declares variables in the scope of an `if` statement in two places: in the `main` function,
and in the `readNumber` function.

Notice also that the variable can be used at any place in the `if` statement: in the condition, in the "then" block, and
in the `else` block. But the variable is not defined outside (before or after) the `if` statement. Trying to use it
outside of that scope would result in an `undefined` compiler error.

Finally, for completeness, notice that other variables, like `quantity` and `reader`, are defined in the scope of a
function. That means that those variables can be used inside of that function, but they are not "visible" i.e. they
can't be referred to from outside that function.

## switch

The `switch` statement also allows declaring a variable in its scope, like this:

```go
switch variable := value; variable {
case expression:
  doSomething()
}
```

For example:

```go
package main

import (
  "bufio"
  "fmt"
  "os"
  "strings"
)

func main() {
  fmt.Print("Which direction? ")
  switch direction := readString(); direction {
  case "north":
    fmt.Printf("Far up %v you see a mountain range.\n", direction)
  case "south":
    fmt.Printf("Looking %v you see sand all the way to the horizon.\n", direction)
  case "east":
    fmt.Printf("A short distance %v you see a house by a tree.\n", direction)
  case "west":
    fmt.Printf("Looking %v you see the shore.\n", direction)
  default:
    fmt.Printf("%v is not a valid direction.\n", direction)
  }
}

func readString() string {
  reader := bufio.NewReader(os.Stdin)
  rawInput, _ := reader.ReadString('\n')
  input := strings.TrimSuffix(rawInput, "\n")
  return input
}
```

Source: [learning-go/shorthand-scoped-var/switch.go](https://github.com/fernandoacorreia/learning-go/blob/b5922b21e5a4dba83fa7b7f96c01b76b4fb00de1/shorthand-scoped-var/switch.go)

Sample output:

```
Which direction? north
Far up north you see a mountain range.
```

Notice how the `direction` variable is declared in the scope of the `switch` statement, and how it is used in the
different conditions inside of that statement.

## for

One or more variables can be declared in the "init" statement of a for loop, like this:

```go
for variable := value; condition; post-statement {
  doSomething()
}
```

For example:

```go
package main

import (
  "bufio"
  "fmt"
  "os"
  "strconv"
  "strings"
)

func main() {
  iterations := readNumber("Number of iterations")
  sum := 0
  for i := 1; i <= iterations; i++ {
    sum += i
  }
  fmt.Println(sum)
}

func readNumber(label string) int {
  fmt.Print(label + "? ")
  reader := bufio.NewReader(os.Stdin)
  rawInput, _ := reader.ReadString('\n')
  input := strings.TrimSuffix(rawInput, "\n")
  if result, err := strconv.Atoi(input); err == nil {
    return result
  }
  panic("Invalid input.")
}
```

Source: [learning-go/shorthand-scoped-var/for.go](https://github.com/fernandoacorreia/learning-go/blob/fba054e5a93ce06d7f1f71e153ff9b24580568dd/shorthand-scoped-var/for.go)

This program produces an output like this:

```
Number of iterations? 4
10
```

It's also possible to declare more than one variable inside of a for loop:

```go
package main

import (
  "fmt"
)

func main() {
  fruits := map[string]string{"a": "apple", "b": "banana"}
  for key, value := range fruits {
    fmt.Printf("%s is for %s.\n", key, value)
  }
}
```

Source: [learning-go/shorthand-scoped-var/for-map.go](https://github.com/fernandoacorreia/learning-go/blob/4e9006b7289ab5cadd3184e8ecd064cb932c0688/shorthand-scoped-var/for-map.go)

Output:

```
a is for apple.
b is for banana.
```

Notice how the variables `key` and `value` are declared in the scope of the `for` loop and are used in its body.

# Takeaways

- Declaring values in the smallest possible scope makes programs easier to understand and reduces the room for errors.
- Variables can be declared via shorthand notation in statements like `if`, `switch` and `for`.
- Variables can de used only in the scope in which they are declared. Their identifiers don't "leak" out of that scope.
