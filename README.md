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
- 

### Zero values
- 

### Type conversions
- 

### Type inference
- 

### Constants
- 

### Numeric constants
- 

## Go basics (Flow control statements: for, if, else, switch, and defer)



## Go basics (More types: structs, slices, and maps)

## Methods and interfaces

## Generics

## References
- [1] https://go.dev/tour/basics/
