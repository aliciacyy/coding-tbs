---
label: Go
---

### Packages
Programs start running in package main.

### Exported names
In Go, a name is exported if it begins with a capital letter.

### Variables
- The var statement declares a list of variables; as in function argument lists, the type is last.
- Inside a function, the := short assignment statement can be used in place of a var declaration with implicit type.

### Types
- bool
- string
- int  int8  int16  int32  int64
- uint uint8 uint16 uint32 uint64 uintptr
- byte // alias for uint8
- rune // alias for int32
- float32 float64
- complex64 complex128

### Type conversions
The expression T(v) converts the value v to the type T.

### Type inference
When declaring a variable without specifying an explicit type (either by using the := syntax or var = expression syntax), the variable's type is inferred from the value on the right hand side.

### Constants
- Constants are declared like variables, but with the const keyword.
- Constants can be character, string, boolean, or numeric values.
- Constants cannot be declared using the := syntax.


### For loops
```
for i := 0; i < 10; i++ {
    sum += i
}

// while true
for {
}
```

### Switch
No need break statement and switch cases need not be constants.
```
switch os := runtime.GOOS; os {
case "darwin":
    fmt.Println("OS X.")
case "linux":
    fmt.Println("Linux.")
default:
    // freebsd, openbsd,
    // plan9, windows...
    fmt.Printf("%s.\n", os)
}
```

### Defer
A defer statement defers the execution of a function until the surrounding function returns.

`defer fmt.Println("world")`

### Struct
```
type Vertex struct {
	X int
	Y int
}

v := Vertex{1, 2}
```

### Arrays
An array's length is part of its type, so arrays cannot be resized.
```
var a [10]int
```

### Slice
A slice is a dynamically-sized, flexible view into the elements of an array
- Changing the elements of a slice modifies the corresponding elements of its underlying array.

```
var s []int = primes[1:4]
r := []bool{true, false, true, true, false, true}

// The make function allocates a zeroed array and returns a slice that refers to that array
a := make([]int, 5)  // len(a)=5

// Appending to slice
s = append(s, 2, 3, 4)
```

### Range
The range form of the for loop iterates over a slice or map.

i is index, v is copy of element
```
for i, v := range pow {
    fmt.Printf("2**%d = %d\n", i, v)
}

// skip index or value
for i, _ := range pow
for _, value := range pow
```

### Maps
A map maps keys to values.

```
type Vertex struct {
	Lat, Long float64
}

var m map[string]Vertex

m = make(map[string]Vertex)
m["Bell Labs"] = Vertex{
    40.68433, -74.39967,
}

var m = map[string]Vertex{
	"Bell Labs": {40.68433, -74.39967},
	"Google":    {37.42202, -122.08408},
}

// insert
m[key] = elem

// retrieve
elem = m[key]

// delete
delete(m, key)

// test key is present
elem, ok := m[key]
```

### Function values
Can be used as function arguments and return values.

```
func compute(fn func(float64, float64) float64) float64 {
	return fn(3, 4)
}
hypot := func(x, y float64) float64 {
    return math.Sqrt(x*x + y*y)
}
fmt.Println(hypot(5, 12))
```

### Function closures
A closure is a function value that references variables from outside its body.
```
func adder() func(int) int {
	sum := 0
	return func(x int) int {
		sum += x
		return sum
	}
}
pos, neg := adder(), adder()
for i := 0; i < 10; i++ {
    fmt.Println(
        pos(i),
        neg(-2*i),
    )
}
```

### Methods on types
- Go does not have classes. However, you can define methods on types.
- A method is a function with a special receiver argument.
- In this example, the Abs method has a receiver of type Vertex named v.
- You can declare a method on non-struct types too.
- You can only declare a method with a receiver whose type is defined in the same package as the method. You cannot declare a method with a receiver whose type is defined in another package (which includes the built-in types such as int).

```
func (v Vertex) Abs() float64 {
	return math.Sqrt(v.X*v.X + v.Y*v.Y)
}
v := Vertex{3, 4}
v.Abs()
```

### Pointer receivers
- The receiver type has the literal syntax *T for some type T
- Methods with pointer receivers can modify the value to which the receiver points (as Scale does here). Since methods often need to modify their receiver, pointer receivers are more common than value receivers.

#### Reasons
- The first is so that the method can modify the value that its receiver points to.
- The second is to avoid copying the value on each method call. This can be more efficient if the receiver is a large struct, for example.

### Interface
- An interface type is defined as a set of method signatures.
- A type implements an interface by implementing its methods. There is no explicit declaration of intent, no "implements" keyword.

```
type Abser interface {
	Abs() float64
}

type MyFloat float64

func (f MyFloat) Abs() float64 {
	if f < 0 {
		return float64(-f)
	}
	return float64(f)
}

var a Abser
f := MyFloat(-math.Sqrt2)
a = f  // a MyFloat implements Abser
```

### Type assertions
- A type assertion provides access to an interface value's underlying concrete value.
```
t, ok := i.(T)
```
This statement asserts that the interface value i holds the concrete type T and assigns the underlying T value to the variable t.

### Type switch
A type switch is a construct that permits several type assertions in series.
```
switch v := i.(type) {
case T:
    // here v has type T
case S:
    // here v has type S
default:
    // no match; here v has the same type as i
}
```

### Errors
Go programs express error state with error values.

```
type error interface {
    Error() string
}

i, err := strconv.Atoi("42")
if err != nil {
    fmt.Printf("couldn't convert number: %v\n", err)
    return
}

func (e *MyError) Error() string {
	return fmt.Sprintf("at %v, %s",
		e.When, e.What)
}

func run() error {
	return &MyError{
		time.Now(),
		"it didn't work",
	}
}
```
A nil error denotes success; a non-nil error denotes failure.

### Type parameters
Go functions can be written to work on multiple types using type parameters. The type parameters of a function appear between brackets, before the function's arguments.
```
func Index[T comparable](s []T, x T) int
```
This declaration means that s is a slice of any type T that fulfills the built-in constraint comparable. x is also a value of the same type.

### Generic types
In addition to generic functions, Go also supports generic types. A type can be parameterized with a type parameter, which could be useful for implementing generic data structures.
```
// List represents a singly-linked list that holds
// values of any type.
type List[T any] struct {
	next *List[T]
	val  T
}
```

### Goroutines
A goroutine is a lightweight thread managed by the Go runtime.
```
go f(x, y, z) // starts goroutine
```

### Other readings
- https://go.dev/doc/effective_go
- https://go.dev/doc/tutorial/