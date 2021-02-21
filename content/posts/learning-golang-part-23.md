---
title: "Learning Golang: Random numbers"
date: 2021-02-20T23:29:42Z
tags: ["golang"]
categories: ["learning golang"]
---

This is part 23 of my [journey](/categories/learning-golang/) learning Golang.

# Random number generators

For some kinds of programs, like simulations, games, or test code, it is useful to be able to generate unpredictable
sequences of numbers.

While generating truly random numbers is a hard problem (see [RANDOM.ORG](https://www.random.org/)), a common
alternative is to use a [pseudorandom number generator](https://en.wikipedia.org/wiki/Pseudorandom_number_generator).

Go has a package for generating pseudo-random numbers: [rand](https://golang.org/pkg/math/rand/).

# Random integer

The `Int()` function from the `rand` package returns a non-negative pseudo-random `int`.

For example:

```go
package main

import (
  "fmt"
  "math/rand"
  "time"
)

func main() {
  rand.Seed(time.Now().UnixNano())
  for i := 0; i < 3; i++ {
    r := rand.Int()
    fmt.Println(r)
  }
}
```

Source: [learning-go/random/random-integer.go](https://github.com/fernandoacorreia/learning-go/blob/master/random/random-integer.go)

When executed it produces output like this:

```
❯ bin/go run ./random/random-integer.go
7844980600027973356
3488658292559818292
3150213459654129095

❯ bin/go run ./random/random-integer.go
8417580983999923480
7072937072426873398
8910705581888374081
```

The `Int()` function is being called 3 times, and each time it produces a different value.

Notice that the `Seed()` function is being used to initialize the pseudo-random generator with an integer value
corresponding to the current time. That makes the generator produce a different sequence each time the program is
executed. Without that, it would always use the same seed value, and produce the same numbers.

Keep in mind that the pseudo-random number generator is deterministic, not truly random. That's why if we want different
results, we must configure it to start from different starting points.

# Cryptographically strong random seed

Using the current time as random seed, like the program above does, is not good enough if the random numbers that will
be generated need to be hard to predict or tamper with. See [this Stack Overflow answer](https://stackoverflow.com/a/54491783/376366)
for a brief explanation of the problem.

The `crypto/rand` package implements a cryptographically secure random number generator. It is based on secure random
number generators provided by the underlying operating system. Read about [entropy](https://en.wikipedia.org/wiki/Entropy_(computing))
to learn more.

For instance take a look at this program:

```go
package main

import (
  "encoding/binary"
  "fmt"
  crypto_rand "crypto/rand"
  math_rand "math/rand"
)

func main() {
  seedRandomizer()
  for i := 0; i < 3; i++ {
    r := math_rand.Int()
    fmt.Println(r)
  }
}

// Based on John Leidegren's code at https://stackoverflow.com/a/54491783/376366
func seedRandomizer() {
    var b [8]byte
    _, err := crypto_rand.Read(b[:])
    if err != nil {
        panic("cannot seed math/rand package with cryptographically secure random number generator")
    }
    math_rand.Seed(int64(binary.LittleEndian.Uint64(b[:])))
}
```

Source: [learning-go/random/random-integer-secure.go](https://github.com/fernandoacorreia/learning-go/blob/e2b3dda0bcbc10c64d8bdc4a6868ce66ed3c7fc4/random/random-integer-secure.go)

The `seedRandomizer` function gets 8 strongly random bytes using `crypto/rand`'s `Read` function and uses that to seed `math/rand`'s random number generator. That makes it **extremely** difficult to predict or manipulate the numbers that will be generated, with no impact on the generator's performace.

# Random integer on a range

The `Intn` function generates a random integer greater than or equal to 0 and less than an upper limit. To generate
integers in any given range, just shift the range by adding a padding to it.

For instance:

```go
package main

import (
  "encoding/binary"
  "fmt"
  crypto_rand "crypto/rand"
  math_rand "math/rand"
)

func main() {
  seedRandomizer()
  for i := 0; i < 30; i++ {
    fmt.Printf("%v ", randomInt(1, 10))
  }
  fmt.Printf("\n")
}

func randomInt(min, max int) int {
  return min + math_rand.Intn(max - min + 1)
}

// Based on John Leidegren's code at https://stackoverflow.com/a/54491783/376366
func seedRandomizer() {
    var b [8]byte
    _, err := crypto_rand.Read(b[:])
    if err != nil {
        panic("cannot seed math/rand package with cryptographically secure random number generator")
    }
    math_rand.Seed(int64(binary.LittleEndian.Uint64(b[:])))
}
```

Source: [learning-go/random/range.go](https://github.com/fernandoacorreia/learning-go/blob/5b0196ca831a38e8852e56147e4dd2f2a883948c/random/range.go)

Notice how the `randomInt` function adds `min` to offset the lower limit of `Intn` (which is 0) and how it sets the
upper limit to the number of possible values.

Sample output:

```
1 9 2 7 10 1 4 9 1 4 5 7 5 4 5 9 8 2 1 9 9 8 5 10 3 8 4 10 5 6
```

# Random string

An easy way to generate a string of random characters is to generate random numbers that correspond to the desired
characters in the [ASCII chart](https://en.wikipedia.org/wiki/ASCII#Printable_characters).

For example this program will print strings composed of random lowercase letters:

```go
package main

import (
  "encoding/binary"
  "fmt"
  crypto_rand "crypto/rand"
  math_rand "math/rand"
)

func main() {
  seedRandomizer()
  for i := 0; i < 3; i++ {
    fmt.Println(randomString(20))
  }
}

func randomInt(min, max int) int {
  return min + math_rand.Intn(max - min + 1)
}

// Based on Flavio Copes's code at https://flaviocopes.com/go-random/
func randomString(length int) string {
  bytes := make([]byte, length)
  for i := 0; i < length; i++ {
    bytes[i] = byte(randomInt(97, 122))
  }
  return string(bytes)
}

// Based on John Leidegren's code at https://stackoverflow.com/a/54491783/376366
func seedRandomizer() {
  var b [8]byte
  _, err := crypto_rand.Read(b[:])
  if err != nil {
    panic("cannot seed math/rand package with cryptographically secure random number generator")
  }
  math_rand.Seed(int64(binary.LittleEndian.Uint64(b[:])))
}
```

Source: [learning-go/random/strings.go](https://github.com/fernandoacorreia/learning-go/blob/8ebcb262bb43e818f7eedd3451da01b6e06807a9/random/strings.go)

Sample output:

```
awmckozkhqkullghvlga
mhevzjivybulgfcocbnd
sekxlbauktzloghkfecz
```

# Random floating point numbers

The `Float64` function will return pseudo-random floating point numbers greater than or equal to 0 and less than 1.

For example:

```go
package main

import (
  "encoding/binary"
  "fmt"
  crypto_rand "crypto/rand"
  math_rand "math/rand"
)

func main() {
  seedRandomizer()
  for i := 0; i < 3; i++ {
    r := math_rand.Float64()
    fmt.Println(r)
  }
}

// Based on John Leidegren's code at https://stackoverflow.com/a/54491783/376366
func seedRandomizer() {
  var b [8]byte
  _, err := crypto_rand.Read(b[:])
  if err != nil {
    panic("cannot seed math/rand package with cryptographically secure random number generator")
  }
  math_rand.Seed(int64(binary.LittleEndian.Uint64(b[:])))
}
```

Sample output:

```
0.5797031300913683
0.1786276285370312
0.3732865775928763
```

See the [rand package documentation](https://golang.org/pkg/math/rand/) for other variations like:
- `Float32` returns a pseudo-random number as a `float32`.
- `ExpFloat64` returns an exponentially distributed `float64`.
- `NormFloat64` returns a normally distributed `float64`.

# Takeaways
- The [math/rand package](https://golang.org/pkg/math/rand/) has functions for generating random integer and floating-point numbers and doing related operations like permutations and shuffling.
- The [crypto/rand package](https://golang.org/pkg/crypto/rand/) implements a cryptographically secure random number generator. It can be used for security-sensitive applications and it is handy for seeding a `math/rand` generator. See [this article](https://blog.gopheracademy.com/advent-2017/a-tale-of-two-rands/) for a discussion of the trade-offs between the `math` and `crypto` `rand` packages.
- Random numbers can easily be used to generate random values of more complex types.
