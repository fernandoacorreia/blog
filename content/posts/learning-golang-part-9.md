---
title: "Learning Golang: Basic data types" # Title of the blog post.
date: 2020-08-26T03:29:48Z
tags: ["golang"]
categories: ["learning golang"]
# description: "Article description." # Description used for search engine.
# featured: true # Sets if post is a featured post, making appear on the home page side bar.
# toc: false # Controls if a table of contents should be generated for first-level links automatically.
# menu: main
# featureImage: "/images/path/file.jpg" # Sets featured image on blog post.
# thumbnail: "/images/path/thumbnail.png" # Sets thumbnail image appearing inside card on homepage.
# shareImage: "/images/path/share.png" # Designate a separate image for social media sharing.
# codeMaxLines: 10 # Override global value for how many lines within a code block before auto-collapsing.
# codeLineNumbers: false # Override global value for showing of line numbers within code block.
# figurePositionShow: true # Override global value for showing the figure label.
# categories:
#   - Technology
---

This is part 9 of my [journey](/categories/learning-golang/) learning Golang.

Data types are a designation by a programming language about the kind of values that are being stored.

Go has several basic data types built in. This article explores boolean, numeric and string data types. See [Go's documentation](https://golang.org/ref/spec#Boolean_types) for more details.

# Boolean data type

Boolean values can be either `false` (equivalent to 0) or `true` (equivalent to 1). Although in principle they only require
1 bit of storage, Go uses a byte for convenience reasons.

| Data type | Number of bits | Minimum value | Maximum value  |
| :-------- | -------------: | ------------: | -------------: |
| bool      | 8              | `false`       | `true`         |

# Numeric data types

There are three categories of numeric data types in Go:
- Integer (whole numbers)
- Floating point (numbers with a fractionary part)
- Complex (imaginary numbers)

## Integer numbers

These represent whole numbers. Integer data types have different lenghts and can be signed or unsigned:

| Data type | Number of bits | Minimum value              | Maximum value              |
| :-------- | -------------: | -------------------------: | -------------------------: |
| int8      | 8              | -128                       | 127                        |
| int16     | 16             | -32,768                    | 32,767                     |
| int32     | 32             | -2,147,483,648             | 2,147,483,647              |
| int64     | 64             | -9,223,372,036,854,775,808 | 9,223,372,036,854,775,807  |
| uint8     | 8              | 0                          | 255                        |
| uint16    | 16             | 0                          | 65,535                     |
| uint32    | 32             | 0                          | 4,294,967,295              |
| uint64    | 64             | 0                          | 18,446,744,073,709,551,615 |

There are also aliases for some of the above data types:

- `byte`: alias for `uint8`
- `rune`: alias for `int32` (represents a [Unicode code point](https://www.geeksforgeeks.org/rune-in-golang/) (loosely, a "character")
- `int`: alias for `int32` or `int64` depending on the platform

## Floating-point numbers

These represent numbers that may have a fractional part. They don't have a minimum or maximum value, but they have
different levels of precision (accuracy) for representing numbers.

| Data type | Number of bits | Precision | Exponent length | Fraction length |
| :-------- | -------------: | :-------- | --------------: | --------------: |
| float32   | 32             | [single](https://en.wikipedia.org/wiki/Single-precision_floating-point_format#IEEE_754_single-precision_binary_floating-point_format:_binary32) | 8 | 23 |
| float64   | 64             | [double](https://en.wikipedia.org/wiki/Double-precision_floating-point_format#IEEE_754_double-precision_binary_floating-point_format:_binary64) | 11 | 52 |

Hint: Floating point data types are binary numbers. They can present rounding errors when storing decimal numbers. For
applications that require guaranteed precision for decimal values (like currency) see the [decimal](https://godoc.org/github.com/shopspring/decimal) package.

## Complex numbers

These represent numbers with an [imaginary part](https://en.wikipedia.org/wiki/Complex_number). They're useful for
computations on 2-dimensional space and calculations involving square roots.

| Data type  | Number of bits | Range |
| :--------- | -------------: | :-------- |
| complex64  | 64             | complex numbers with float32 real and imaginary parts |
| complex128 | 128            | complex numbers with float64 real and imaginary parts |

# String

Go strings are "a read-only slice of bytes", i.e. a contiguous sequence of bytes -- `uint8` integers.

It's important to notice that these can be arbitrary bytes. They don't have to be Unicode code points and they don't
have to be encoded as UTF-8 or any other encoding. That said, Go's library functions assume that strings are encoded as
UTF-8. See [this blog post](https://blog.golang.org/strings) for more details.

| Data type | Content       | Length                 |
| :-------- | :------------ | :--------------------- |
| string    | bytes (uint8) | 0 to maximum int value |

# Takeaways

Go offers several built-in data types. Each one is suited for different use cases:
- `bool` for boolean logic (true and false values)
- signed and unsigned integers of different sizes for fast, memory-efficient arithmetic with whole numbers
- two levels of precision for numbers with a fractional part
- two different lengths for complex numbers
- `string` for sequences of bytes

This level of specialization (particularly of the numeric data types) can be overwhelming at first, and requires understanding the types and ranges of data that
the aplication will handle. The trade-off is being able to produce faster-running programs that require less memory in
comparison with equivalent programs in languages with a more lax type system.
