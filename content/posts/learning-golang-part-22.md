---
title: "Learning Golang: Scoped shorthand variable declaration" # Title of the blog post.
date: 2021-02-12T04:04:15Z # Date of post creation.
tags: ["golang"]
categories: ["learning golang"]
---

This is part 21 of my [journey](/categories/learning-golang/) learning Golang.

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

## if statement shorthand scoped variable declaration

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
