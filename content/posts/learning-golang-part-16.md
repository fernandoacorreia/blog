---
title: "Learning Golang: Printf" # Title of the blog post.
date: 2020-09-15T03:39:46Z # Date of post creation.
tags: ["golang"]
categories: ["learning golang"]
---

This is part 16 of my [journey](/categories/learning-golang/) learning Golang.

# The Printf method

The [Printf](https://golang.org/pkg/fmt/#Printf) method from the [fmt](https://golang.org/pkg/fmt/) package writes a
formatted string to standard output.

`Printf` makes it possible to **interpolate** strings. This is done by leaving placeholders in a string, and using
values to fill in these placeholders.

# Printf syntax

`Printf` accepts a string argument, potentially with formatting placeholders, and zero or more value arguments. For
example:

```go
package main

import (
  "fmt"
)

func main() {
  answer := "C"
  fmt.Printf("Is %v your final answer?", answer)
}
```

prints out:

```
Is C your final answer?
```

Keep in mind that, like `Print`, `Printf` does not automatically add a newline character.

The `%v` portion of the first argument is the placeholder for a "value".

# Multiple placeholders

The "format specifier" i.e. the first argument can contain an arbitrary number of placeholders. This way, multiple
values can be printed out with a single statement. This is one use case where `Printf` shines over `Print`. To achieve
the same thing with `Print` several statements would be required. Additionally `Print` doesn't support any formatting
other than the default string representation of its argument.

For example:

```go
package main

import (
  "fmt"
)

func main() {
  const name, age, pronoun, profession = "Kim", 22, "She", "woodworker"
  fmt.Printf("%s is %d years old.\n", name, age)
  fmt.Printf("%s is a %s.\n", pronoun, profession)
}
```

prints out:

```
Kim is 22 years old.
She is a woodworker.
```

A newline character is printed after each of these lines, because it was explicitly included in the format specifier.

Notice that the placeholders used were `%s` (for string) and `%d` (for decimal i.e. base 10 integer number).

# Verbs

The placeholders in the format specifier are called "verbs". To view a full list of supported format verbs, see the [fmt
package's documentation](https://golang.org/pkg/fmt/#pkg-overview).

These are some of the most common ones:

| Verb | Meaning |
| :--- | :------ |
| %v   | the value in a default format |
| %+v  | a default representation of structs, with field names |
| %#v  | a Go-syntax representation of the value |
| %T   | a Go-syntax representation of the type of the value |
| %d   | an integer value in decimal (base 10) representation |
| %E   | scientific notation, e.g. -1.234456E+78 |
| %f   | decimal point but no exponent, e.g. 123.456 |
| %s   | a string or slice (without interpreting the bytes) |
| %q   | a double-quoted string safely escaped with Go syntax |

To print a literal `%` (percent) symbol escape it like this: `%%`.

# Width and precision

The width of each formatted value can be specified by an optional decimal number immediately preceding the verb.

The precision can be specified after the (optional) width by a period followed by a decimal number.

This example shows some common uses of these modifiers:

```go
package main

import (
  "fmt"
)

func main() {
  const s, n = "Pi", 3.1415926535
  fmt.Printf("'%v'='%v'\n", s, n)
  fmt.Printf("'%s'='%f'\n", s, n)
  fmt.Printf("'%10s'='%1.4f'\n", s, n)
  fmt.Printf("'%-10s'='%1.1f'\n", s, n)
}
```

this is the output:

```
'Pi'='3.1415926535'
'Pi'='3.141593'
'        Pi'='3.1416'
'Pi        '='3.1'
```

Note that in the example above the single quotes (`'`) are just regular characters to help visualize where each formatted
value starts and ends. They have no special meaning for the `Printf` method.

There are many more special cases and flags than would fit an introductory article. The package's
[documentation](https://golang.org/pkg/fmt/#pkg-overview) is a great place to find out what all the possibilities are.

# Takeaways

`Printf` is an extremely useful and flexible method. It resembles in versatility the original `printf` function of the C
language, but it is simpler to use.

Do you often use `Printf`? What other tips would you highlight?
