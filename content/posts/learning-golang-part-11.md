---
title: "Learning Golang: Variables" # Title of the blog post.
date: 2020-09-06T18:13:20Z # Date of post creation.
tags: ["golang"]
categories: ["learning golang"]
---

This is part 11 of my [journey](/categories/learning-golang/) learning Golang.

# Variables

A variable is a named value that can change during the execution of a program. The difference from a constant (which is
also a named value) is that a variable's value can be modified at run time.

# Variable declarations

In Go, variables are declared following this pattern: `var` {identifier} {type}. Examples:

```go
var songName string
var lengthOfSong uint16
var isMusicOver bool
var songRating float32
```

# Zero values

If a value is not assigned to the variable when it is declared (like above) then it is initialized with a "zero value".
The actual value depends on the data type. Generally:

- 0 for numeric data types
- `false` for the `boolean` data type
- empty string (`""`) for `string` data type

# Default values

The initial value of a variable can be assigned when it is declared:

```go
var shoppingCartQuantity = 1
var shoppingCartItemName = "cupholder"
var shoppingCartPrice = 19.99
var shoppingCartExtendedWarranty = true
```

# Defining multiple variables

Go has a shorthand for declaring several variables in a single statement:

```go
var (
  a = 5
  b = 10
  c = 15
)
```

Use the keyword `var` (or `const`) followed by parentheses with each variable on its own line.

# Shorthand declaration

The `:=` symbol is a shorthand for declaring a variable and assigning a default value. The type of the variable is
inferred from the type of the value, instead of being explicitly declared.

Example:

```go
package main

import (
  "fmt"
)

func main() {
  message := "Hello, world!"
  fmt.Println(message)
}
```

Go offers another way to declare and initialize a variable inferring its type:

```go
package main

import (
  "fmt"
)

func main() {
  var planet = "Earth"        // Inferred type: string
  var radiusInKm = 6371.009   // Inferred type: float64
  var daysInTheYear = 365     // Inferred type: int (int64 or int32)
  var hasMoon = true          // Inferred type: boolean
  fmt.Printf("%T %T %T %T\n", planet, radiusInKm, daysInTheYear, hasMoon)
}
```

The code above prints:

```
string float64 int bool
```

# Updating a variable

The `=` symbol assigns a new value to a variable based on the expression at the right side of the statement (i.e. after
"="). `=` is called the "assignment operator". It is the same operator that was used above to assign default values when
a variable was declared. It can also be used at later parts of the code for updating the value of the variable (i.e.
assigning a new value to it).

Example:

```go
package main

import (
  "fmt"
)

func main() {
  var count uint64
  fmt.Println(count)
  count = count + 1
  fmt.Println(count)
  count += 1
  fmt.Println(count)
  count = 99
  fmt.Println(count)
}
```

This will print:

```
0
1
2
99
```

The first value (0) is the "zero value" for numeric data types and it is the initial value of a numeric variable unless
a different default value is set in the `var` statement.

The second value (1) is the result of the expression `count + 1`.

The third value (2) is the result of the expression `count + 1`. The `+=` symbol is a shorthand for an arithmetic
expression based on the variable's current value.

The third value (99) is the result of the expression `99` (i.e. you can assign any value to the variable; you're not
limited to arithmetic expressions based on the previous value).
