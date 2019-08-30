# General

## Environment

```
Go doesn't support environment variables GOROOT and GOPATH to contain a tilde `~`.

cat >> ~/.environ
export GOARCH="amd64"
export GOBIN="/home/mickael/.local/go-path/bin"
export GOPATH="/home/mickael/.local/go-path"
export GOROOT="/home/mickael/.local/go-lang-root"
export PATH="$GOROOT/bin:$GOBIN:~/bin:/usr/local/bin:/usr/bin:/bin:/usr/local/games:/usr/games
```

```go
package main

import (
    // string
)

func main() {
    // Do something
}
```

A `defer` allows to execute statements at the end of function where it's declared.

Symbols that begin with a capitalized letter are exported.

```go

func add(first, second int) (result int) {
    result = first + second
    return
}
```

Styling: `go fmt ./...`

# Module imports

You can't import locally to your directory, you're sources ought to live in `$GOROOT`. 

When you use dependencies that are to be fetched, you have to run `go get -t ./...`.

# Variable

Variables are initialized by default.

* `var` to declare variables
* `const` to declare a constant variable (equivalent to C++ constexpr)
* `=` is used to initialize
* `:=` is used to assign

Cast style is C++ ctor style.

Type can be inferred instead of explicited when there is a typed value assigned to a
variable.

## Printing

```go
import "fmt"

fmt.Println(v)
```

To customize the output of your type, overload `String() string` function:

```go
import "fmt"
func (node *Node) String() (output string) {
	output = fmt.Sprintf("'%s' ", node.payload)

    return
}
```


## Structures

```go
type Person struct {
    name string
}
```

Type composition:

```go
type T1 struct {
}

type T2 struct {
}

type T3 struct {
    name string
    *T1
    *T2
}

```

## Interfaces

```go
type TypeName interface {
    MethodsName() # Method signature
}

type Target struct {
}

func (self *TargetType) MethodsName() {
}
```

Interfaces can be agglutinated:

```go
type I1 {
}

type I2 {
}

type I3 {
    I1
    I2
}

```

## Allocation

Variables are usually automatic, but you can allocate to get a pointer. Anyway, getting
an address from a variable will make it a dynamic reference.

```go
// Allocate and initialize to type's zero value
age = new(int)
```

```go
// Allocate and initialize to a composite type
person = &Person{"Mickaël", 180, 125}
person = &Person{name: "Mickaël", size: 180, weight: 125}
```

The allocated memory is freed by garbage collection, when no references exist anymore on
the allocated memory.

## Array and slices

```go
var myslice int[]   // Slices are std::vector (dynamic size)
                    // pass by refence behaviour
var myarray int[12] // Arrays are std::array (static size)
                    // pass by copy behaviour
```

```go
package main

import (
	"fmt"
)

func main() {
	var p [20]int
	p[10] = 42
	fmt.Printf("%v\n", p)

	var size = 20
	var v = make([]int, size) // makes a slice
	v[10] = 42
	fmt.Printf("%v\n", v)
}
```

## Maps

To explore `map[keyType]valueType`

# Functions

Keyword `func`

```go
func (s Struct) name(args ...interface{}) (output outType, err error) {

    errType := YoloError
}
```

# Spread syntax

```go
func do(v ...MyType) # Collecting
...v # Spread shit
```

# Flow

```go
if condition {
    // if condition's true
}

if init; condition {
    // if condition's true
}

for {
}

for condition {
}

for init; condition; post {
}

for assignement {
    // loop over the element of a collection
}

// Not a true switch, it's syntax sugar for if-elseif
switch {
case condition1:
    //
case condition2:
    //
}

switch var1 {
case val1, val2:
    //
}
```

# Testing

Lauch test suite: `go test -v ./...`

The language provided utility is dumb, not expressive, and fail to help provinding good
tests. They are designed from the perspective of a Go plumber, not a feature maker.

Some additional framework worth exploring:

- Ginkgo (BDD)
- Gomega (Assertions)
