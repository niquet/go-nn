# Go Notes
This repository is a collection of personal notes on Go, covering various basic concepts, syntax, and best practices. It serves as a (personal) resource for learning and practicing Go programming, providing a comprehensive (enough) understanding of the language's fundamentals and practical applications.

## Table of contents

## Getting started

### The Go Playground
- https://go.dev/blog/playground

### Installing Go

### Hello, world!
- [Visit this example in the Go Playground](https://go.dev/play/p/-MKUWeDBml7)
```go
package main

import "fmt"

func main() {
	fmt.Println("Hello, world!")
}
```

## Go basics (Packages, variables, and functions)

### Packages
- EveryGo program is made up of packages [1]
- (Executable) Programs run in package `main` [1]
- Programs use packages by import paths [1]
- Convention – package name is the same as the last element of the import path [1]

### Imports
- Import statements are written as such [1]
```go
import "fmt"
import "math"
```

- It is good style to group imports into a parenthesized ("factored") import statement [1]
- Example above is then written as
```go
import (
    "fmt"
    "math"
)
```

### Exported names
- Names in Go are exported when they begin with a capital letter [1]
- When importing a package, you can refer only to its exported names [1]
- Any unexported names are not accessible from outside the package [1]

### Functions
- A function can take zero or more arguments [1]
- The type comes after the parameter name [1]
- [Visit this example in the Go Playground](https://go.dev/play/p/oMmhdD4U1IO)
```go
package main

import "fmt"

func add(a int, b int) int {
	return a + b
}

func main() {
	fmt.Println(add(15, 37))
}
```

- When two or more consecutive named function parameters share a type, the type can be omitted from all but the last [1]
```go
a int, b int
```
to
```go
a, b int
```

- A function can return any number of results [1]
- [Visit this example in the Go Playground](https://go.dev/play/p/DLbQ49HPv4Q)
```go
package main

import "fmt"

func addAndSub(a int, b int) (int, int) {
	return a + b, a - b
}

func main() {
	fmt.Println(addAndSub(15, 37))
}
```

- Return values may be named [1]
- Named return values are treated as variables defined at the top of the function [1]
- Names of named return values should be used to document the meaning of the return values [1]
- A `return` statement without arguments returns the named return values ("naked" return) [1]
- Naked return statements should only be used in short functions as they can harm readability in longer functions [1]
- [Visit this example in the Go Playground](https://go.dev/play/p/NHQuTq4DvhB)
```go
package main

import "fmt"

func add(a int, b int) (sum int) {
	sum = a + b
	return
}

func main() {
	fmt.Println(add(40, 2))
}
```

### Variables
- `var` statement declares a (list of) variable(s); the type is last [1]
- `var` statement can be at package or function level [1]
- [Visit this example in the Go Playground](https://go.dev/play/p/kcsD53Yxlel)
```go
package main

import "fmt"

var one int

func main() {
	var two, three int
	one = 1
	two = 2
	three = 3

	fmt.Println(one, two, three)
}
```

### Variables with initializers
- A var declaration can include initializers, one per variable [1]
- If an initialzer is present, thee type can be omitted, the variable will take the type of the initializer [1]
- [Visit this example in the Go Playground](https://go.dev/play/p/laaSQ0qR5Pj)
```go
package main

import "fmt"

var one, two int = 1, 2

func main() {
	var three = 3
	var isTrue, helloWorld = true, "Hello, world!"

	fmt.Println(one, two, three, isTrue, helloWorld)
}
```

### Short variable declarations
- Inside of a function, the `:=` short assigment statement (short variable declaration) can be used in place of a `var` declaration with implicit type [1]
- Outside of a function, every statement begins with a keyword (`var`, `func`, etc.); the `:=` is not available [1]
- [Visit this example in the Go Playground](https://go.dev/play/p/zF5twQUWXrR)
```go
package main

import "fmt"

// one, two := 1, 2 is not available
var one, two int = 1, 2

func main() {
	// var three = 3
    three := 3
	// var isTrue, helloWorld = true, "Hello, world!"
    isTrue, helloWorld := true, "Hello, world!"

	fmt.Println(one, two, three, isTrue, helloWorld)
}
```

### Basic types
- bool
- string
- int, int8, int16, int32, int64
- uint, uint8, uint16, uint32, uint64, uintptr
- byte (alias for uint8)
- rune (alias for int32, represents a Unicode code point)
- float32, float64
- complex64, complex128
- The int, uint, and uintptr types are usually 32 bits wide on 32-bit systems and 64 bits wide on 64-bit systems [1]
- When you need an integer value you should use int unless you have a specific reason to use a sized or unsigned integer type [1]

### Zero values
- Variables declared without an explicit initial value are given their _zero value_ [1]
- Zero value is:
  - 0 for numeric types
  - false for boolean type
  - "" (empty string) for string type

### Type conversions
- The expression `T(v)` converts the value `v` to the type `T` [1]
- In Go, assignment between items of different type requires an explicit conversion [1]
- [Visit this example in the Go Playground](https://go.dev/play/p/eojq2nHzkEd)
```go
package main

import "fmt"

func main() {
	a := 3
	b := 7
	f := float64(a*b + a*a - b*b)
	var res int = int(f)
	fmt.Println(a, b, res)
}
```

### Type inference
- When declaring a variable without specifying an explicit type, the variable's type is inferred from the value on the right hand side [1]
- When the right hand side of the declaration is typed, the new variable is of that same type [1]
- [Visit this example in the Go Playground](https://go.dev/play/p/OariO-P_McJ)
```go
package main

import "fmt"

func main() {
	var a int
	b := a

	fmt.Printf("%T %T\n", a, b)
}
```

- When the right hand side of the declaration contains an untyped numeric constant, the type of the new variable depends on the precision of the value [1]
- [Visit this example in the Go Playground](https://go.dev/play/p/9uiCqlhrS0i)
```go
package main

import "fmt"

func main() {
	a := 1
	b := 2.1
	c := 3 + 0i

	fmt.Printf("%T %T %T\n", a, b, c)
}
```

### Constants
- Constants are declared using the `const` keyword [1]
- Constants can be character, string, boolean, or numeric values [1]
- Constants _cannot_ be declared using the `:=` shorthand syntax [1]
- [Visit this example in the Go Playground](https://go.dev/play/p/gCq4wYL2Rxl)
```go
package main

import "fmt"

func main() {
	const a = "Hello, world!"
	const b = 3.14
	const c = true

	fmt.Printf("%T %T %T\n", a, b, c)
}

```

### Numeric constants
- Numeric constants are high-precision values [1]
- An untyped constant takes the type needed by its context [1]

## Go basics (Flow control statements: for, if, else, switch, and defer)

### For
- `for` loop is the only looping construct in Go [1]
- Basic `for` loop has thrree components separated by semicolons [1]:
  - init statement: executed before the first iteration
  - condidtion expression: evaluated before every iteration
  - post statement: executed at the end of every iteration
- init statement is often a short variable declaration [1]
- Variables declared in the init statement are only visible in the scope of the `for` statement [1]
- Loop stops iterating once the boolean condition expression evaluates to `false` [1]
- [Visit this example in the Go Playground](https://go.dev/play/p/Yh8jRtIdbuT)
```go
package main

import "fmt"

func main() {
	sum := 0
	for i := 0; i < 10; i++ {
		sum += i
	}
	fmt.Println(sum)
}
```

- init and post statements are optional
- [Visit this example in the Go Playground](https://go.dev/play/p/-8ihiw0pxlX)
```go
package main

import "fmt"

func main() {
	sum :=1
	// the semicolons (";") an be dropped
	for ; sum < 1000; {
		sum += sum
	}
	fmt.Println(sum)
}
```

- Go doesn't not have a `while` keyword, howver, using Go's `for` without the init and post statements is euqal to a while loop [1]
- [Visit this example in the Go Playground](https://go.dev/play/p/b0CRVhku7eS)
```go
package main

import "fmt"

func main() {
	count := 0
	for count < 1000 {
		count += 1
	}
	fmt.Println(count)
}
```

- The condition expression defaults to true; omitting the loop condition leads to an infinite loop [1]
- [Visit this example in the Go Playground](https://go.dev/play/p/oNIinSe8rFl)
```go
package main

import "fmt"

func main() {
	count := uint32(0)
	var largeNum uint32 = 1<<32 - 1

	for {
		// adding break statement to not loop forever
		if count == largeNum {
			break
		}
		count += 1
	}

	fmt.Println(count)
}
```

### If
- 

## Go basics (More types: structs, slices, and maps)

## Methods and interfaces

## Generics

## References
- [1] https://go.dev/tour/basics/
- [2] https://go.dev/tour/flow/
