---
title: "Learning Golang: if and else" # Title of the blog post.
date: 2020-10-08T04:26:15Z # Date of post creation.
tags: ["golang"]
categories: ["learning golang"]
---

This is part 19 of my [journey](/categories/learning-golang/) learning Golang.

# Conditionals

Any program can be written in terms of three control structures:

- the **sequence structure**, in which expressions are executed in sequence, one after the other, in the order that they are
  written;
- the **selection structure**, in which a statement can be executed or not, depending on some condition; and
- the **iteration structure**, in which statements may be executed repeatedly until a condition becomes true (or false).

Conditionals are selection structures. The provide a way for expressing decision-making in a program. Depending on the
value of an expression, the program may execute (or not) one or more statements.

Go provides two keywords for implementing conditionals: `if` and `switch`. This article focuses on the `if` construct.

# if

The `if` keyword starts a selection statement. It evaluates the boolean expression that immediately follows it. If the
value of the expression is `true`, a block of statements is executed. If the value is `false`, the block os statements
is not executed. The block can contain zero, one or several statements.

For example:

```go
package main

import (
  "fmt"
  "math/rand"
  "time"
)

func main() {
  // Initialize random number generator.
  r := rand.New(rand.NewSource(time.Now().UnixNano()))

  // Generate 2 small integer numbers.
  mine := r.Intn(10)
  yours := r.Intn(10)

  // Print out the random numbers.
  fmt.Println("Mine:", mine)
  fmt.Println("Yours:", yours)

  // Print out whether I won.
  if mine > yours {
    fmt.Println("I win.")
  }
}
```

Source: [learning-go/conditionals/if.go](https://github.com/fernandoacorreia/learning-go/blob/345dfae52c62bee300d4448992ef2cf6b38fe662/conditionals/if.go)

When run repeatedly, the program produces an output like this:

```
❯ bin/go run conditionals/if.go
Mine: 5
Yours: 5

❯ bin/go run conditionals/if.go
Mine: 5
Yours: 0
I win.

❯ bin/go run conditionals/if.go
Mine: 2
Yours: 7
```

Notice than when the value of "mine" is greater than the value of "yours", it prints out "I win." In the other cases (if
it is the same or smaller) it doesn't print any additional message.

Keep in mind that the block of code following the `if` can have as many statements as you need, not just one as in the
example. It can also have no statements -- but in this case it will be rather pointless.

# Comparison operators

Go's [comparison operators](https://www.tutorialspoint.com/go/go_relational_operators.htm) (also called "relational"
operators) are particularly useful for conditional expressions. For example:

| Operator | Meaning |
| :------- | :------ |
| ==       | Equal to |
| !=       | Different from |
| >        | Greather than |
| <        | Less than |
| >=       | Greather than or equal to |
| <=       | Less than or equal to |

These operators compare two arguments (to their left and to their right) and produce a boolean result, i.e. `true` or
`false` depending on whether the condition is true or not.

# else

The `else` keyword, in an `if` statement, executes a block of code if and only if the expression of the `if` statement
was `false`.

For example:

```go
package main

import (
  "fmt"
  "math/rand"
  "time"
)

func main() {
  // Initialize random number generator.
  r := rand.New(rand.NewSource(time.Now().UnixNano()))

  // Generate 2 integer numbers.
  limit := r.Intn(10)
  value := r.Intn(20)

  // Print out the random numbers.
  fmt.Println("Limit:", limit)
  fmt.Println("Value:", value)

  // Print out result of comparison.
  if value > limit {
    fmt.Println("Above limit.")
  } else {
    fmt.Println("Within limit.")
  }
}
```

Source:
[learning-go/conditionals/if-else.go](https://github.com/fernandoacorreia/learning-go/blob/8b2734601cf72a7354397a9e7e1080ca0eacadee/conditionals/if-else.go)

When executed repeatedly, the program will produce output like this:

```
❯ bin/go run conditionals/if-else.go
Limit: 4
Value: 4
Within limit.

❯ bin/go run conditionals/if-else.go
Limit: 9
Value: 7
Within limit.

❯ bin/go run conditionals/if-else.go
Limit: 6
Value: 19
Above limit.
```

Notice that when the value is greater than the limit, it prints out "Above limit." and when the value is less than or
equal to the limit, it prints out "Within limit."

Keep in mind that the blocks of code following the `if` and `else` keywords can have as many statements as you need, not
just one as in the example.

# else if

The `else` keyword can be followed by another `if` statement. The block of the new `if` statement will be executed if the expression of the previous `if` statement was false, and the expression is the new `if` statement is true.

For example:

```go
package main

import (
  "fmt"
  "math/rand"
  "time"
)

func main() {
  // Initialize random number generator.
  r := rand.New(rand.NewSource(time.Now().UnixNano()))

  // Generate 2 integer numbers.
  limit := r.Intn(10)
  value := r.Intn(20)

  // Print out the random numbers.
  fmt.Println("Limit:", limit)
  fmt.Println("Value:", value)

  // Print out result of comparison.
  if value > limit {
    fmt.Println("Above limit.")
  } else if value < limit {
    fmt.Println("Under limit.")
  } else {
    fmt.Println("At the limit.")
  }
}

```

Source:
[learning-go/conditionals/if-else-if.go](https://github.com/fernandoacorreia/learning-go/blob/d0dceab4f8534371c470898298132e62c08abf6c/conditionals/if-else-if.go)

Produces an output like this:

```
❯ bin/go run conditionals/if-else-if.go
Limit: 1
Value: 1
At the limit.

❯ bin/go run conditionals/if-else-if.go
Limit: 8
Value: 14
Above limit.

❯ bin/go run conditionals/if-else-if.go
Limit: 4
Value: 2
Under limit.
```

Notice that when the value is greater than the limit, the block for the first `if` statement is executed; when the value
is less than the limit, the block for the second `if` statement is executed; and when neither of these conditions is
`true`, i.e. when both the value and the limit are the same, the block for the final `else` statement is executed.

Keep in mind that you can chain as many `else if` statements as necessary, each with a different condition the must be
true for its block to be executed. The sequence may or may not have a final `else` clause not followed by a new `if`
statement.

# else if chains

`else if` statements can be chained as many times as necessary. The block for the first condition that evaluates to
`true` will be executed, and the others will be skipped. If no condition is `true`, and there is an `else` clause, its
block will be executed. If there isn't an `else` clause, then no block will be executed for that chain.

For example:

```go
package main

import (
  "os"
  "bufio"
  "fmt"
  "strings"
)

func main() {
  // Ask the user to enter a number.
  reader := bufio.NewReader(os.Stdin)
  fmt.Print("What position did you finish at? ")
  positionInput, _ := reader.ReadString('\n')
  position := strings.TrimSuffix(positionInput, "\n")

  // Print out message for the position.
  if position == "1" {
    fmt.Println("Congrats! You finished in first place.")
  } else if position == "2" {
    fmt.Println("You were a close second.")
  } else if position == "3" {
    fmt.Println("You finished in third.")
  } else {
    fmt.Println("Better luck next time!")
  }
}
```

Source:
[learning-go/conditionals/if-else-chain.go](https://github.com/fernandoacorreia/learning-go/blob/ff5bee3567f191bbd9cc74f655d7d7de8aa09fe2/conditionals/if-else-chain.go)

The program above produces this output:

```
❯ bin/go run ./conditionals/if-else-chain.go
What position did you finish at? 1
Congrats! You finished in first place.

❯ bin/go run ./conditionals/if-else-chain.go
What position did you finish at? 2
You were a close second.

❯ bin/go run ./conditionals/if-else-chain.go
What position did you finish at? 3
You finished in third.

❯ bin/go run ./conditionals/if-else-chain.go
What position did you finish at? 4
Better luck next time!
```

# Takeaways

- Go provides the `if` keyword for creating a selection strucuture that will only execute a block of statements if a
  condition is `true`.
- The optional `else` clause will execute a block of statements if the previous condition was not `true`.
- An `else` clause can start a new `if` statement. That `else` clause (and its `if` statement) will only execute if the
  condition of the preceding `if` statement was `false`.
- Only one block of a sequence of `if`, `else if` and `else` keywords will be executed.
- If no `if` condition was `true`, and no `else` clause was provided, no statement will be executed.
- The program flow will continue on the next statement following the end of the entire sequence of `if`, `else if` and
  `else` blocks.
- the conditions following the `if` can be as complex as necessary. for instance they can use Go's [logical
  operators](/posts/learning-golang-part-20/) (`&&`, `||`, `!`) to combine multiple boolean values.
