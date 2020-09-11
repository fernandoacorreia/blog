---
title: "Learning Golang: Assigning and printing variables" # Title of the blog post.
date: 2020-09-11T03:59:46Z # Date of post creation.
tags: ["golang"]
categories: ["learning golang"]
codeMaxLines: 200
---

This is part 14 of my [journey](/categories/learning-golang/) learning Golang.

As an exercise for Codecademy's [Learn Go](https://www.codecademy.com/learn/learn-go) course, I wrote my second Go
program.

It simulates a catalog for a comic book store.

At this point the course has only covered the most fundamental parts of Go, like variables, simple data types, basic
arithmetic, and printing. Arrays and functions are still out of the picture.

For that reason, the structure of the program is very primitive and there is a lot of repetition (room for improvement).

That still made it a valuable exercise. Some of the concepts that this little program reinforces are:

- Declaring variables of different data types.
- Assigning (and re-assigning) values to variables.
- Doing basic arithmetic.
- Mixing whole numbers arithmetic with fractional numbers arithmetic (data type conversion).
- Printing out variable values along with text literals.

This is the full code:

```go
package main

import(
  "fmt"
)

func main() {
  // Comic book variables
  var publisher, writer, artist, title, genre string
  var year, pageNumber, age int
  var grade, price float32

  // Define first comic book
  title = "Mr. GoToSleep"
  genre = "Mistery"
  writer = "Tracey Hatchet"
  artist = "Jewel Tampson"
  publisher = "DizzyBooks Publishing Inc."
  year = 1997
  pageNumber = 14
  grade = 6.5
  age = 2020 - year
  price = float32(age * pageNumber) * grade / 100.0

  // Print out variables
  fmt.Println(
    title,
    "genre", genre,
    "written by", writer,
    "drawn by", artist,
    "published by", publisher,
    "on", year,
    "containing", pageNumber, "pages",
    "in condition", grade,
    "price", price,
  )

  // Define second comic book
  title = "Epic Vol. 1"
  genre = "SciFi"
  writer = "Ryan N. Shawn"
  artist = "Phoebe Paperclips"
  publisher = "DizzyBooks Publishing Inc."
  year = 2013
  pageNumber = 160
  grade = 9.0
  age = 2020 - year
  price = float32(age * pageNumber) * grade / 100.0

  // Print out variables
  fmt.Println(
    title,
    "genre", genre,
    "written by", writer,
    "drawn by", artist,
    "published by", publisher,
    "on", year,
    "containing", pageNumber, "pages",
    "in condition", grade,
    "price", price,
  )

  // Define third comic book
  title = "Ms. Y"
  genre = "Adventure"
  writer = "Gordon Ryan"
  artist = "Isobelle Leclair"
  publisher = "Astra Books"
  year = 2001
  pageNumber = 47
  grade = 8.5
  age = 2020 - year
  price = float32(age * pageNumber) * grade / 100.0

  // Print out variables
  fmt.Println(
    title,
    "genre", genre,
    "written by", writer,
    "drawn by", artist,
    "published by", publisher,
    "on", year,
    "containing", pageNumber, "pages",
    "in condition", grade,
    "price", price,
  )

}
```

Source: [learning-go/comic-mischief/main.go](https://github.com/fernandoacorreia/learning-go/blob/36daa970169e2096d3ed07b5f7cb8f6525e2558b/comic-mischief/main.go)

The program prints this out:

```
Mr. GoToSleep genre Mistery written by Tracey Hatchet drawn by Jewel Tampson published by DizzyBooks Publishing Inc. on 1997 containing 14 pages in condition 6.5 price 20.93
Epic Vol. 1 genre SciFi written by Ryan N. Shawn drawn by Phoebe Paperclips published by DizzyBooks Publishing Inc. on 2013 containing 160 pages in condition 9 price 100.8
Ms. Y genre Adventure written by Gordon Ryan drawn by Isobelle Leclair published by Astra Books on 2001 containing 47 pages in condition 8.5 price 75.905
```
