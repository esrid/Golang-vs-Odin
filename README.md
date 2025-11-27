# Golang Vs Odin: Syntax Comparison

A quick cheat-sheet comparing the fundamental syntax of the Go and Odin programming languages.

## 📜 Sommaire

* [Naming Convention](#️-naming-convention)
* [Package](#-package)
* [Import](#-import)
* [Basic Types](#-basic-types)
* [Custom Type](#️-custom-type)
* [Enum](#-enum)
* [Variable](#-variable)
* [Function](#-function)
* [If Statement](#-if-statement)
* [Loops](#-loops)
* [Switch](#-switch)

## Naming Convention

* **Odin:** Uses `snake_case` for most identifiers.
* **Go:** Uses `camelCase` (or `PascalCase` for exported identifiers).

## Package
Declare the package on the top of the file, same in both languages.
```
package main
```

# Import

Both use the same keyword

```
import "fmt"
import "log"

// multiple import
import (
  "fmt"
  "log"
)

Odin: 
// Odin does not support multiple import blocks (import (...))
import "core:fmt"
import "core:log"
```


## BASIC Type
Both languages have a concept of a zero value for their types

| Type Category             | Go Types                                      | Odin Types                                      | Notes |
|---------------------------|----------------------------------------------|------------------------------------------------|-------|
| **Boolean**               | bool                                         | bool, b8, b16, b32, b64                        |       |
| **Signed Integer**        | int, int8, int16, int32, int64              | i8, i16, i32, i64, i128, int                  | int is pointer-sized in Odin |
| **Unsigned Integer**      | uint, uint8, uint16, uint32, uint64, uintptr, byte, rune | u8, u16, u32, u64, u128, uint, uintptr       | byte is alias for int8; rune is alias for int32 in both languages |
| **Floating-Point**        | float32, float64                             | f16, f32, f64                                  |       |
| **Complex**               | complex64, complex128                         | complex32, complex64, complex128              |       |
| **Quaternion**            | none                                         | quaternion64, quaternion128, quaternion256    |       |
| **Character / String**    | string, rune                                 | string, string16, cstring, cstring16, rune    | rune alias for int32 |
| **Pointer / Raw Memory**  | pointers (*T)                                | rawptr                                         |       |
| **Generic / Runtime**     | any (via interface{})                        | any, typeid                                    |       |

## Custom Type
```go
package main

import "fmt"

// new type age
type Age int16

// struct
type Person struct {
	name string
	age  Age
}

func (p Person) Age() Age {
    return p.age
}


type Animal struct {
    name string 
    age Age
}

func (a Animal) Age() Age {
    return a.age
}

// interface 
type Ager interface {
    Age() Age
}

func printAge(a Ager) {
    fmt.Println("Age:", a.Age())
}

func main() {
    p := Person{name: "Alice", age: 30}
    dog := Animal{name: "Rex", age: 5}

    printAge(p)
    printAge(dog)
}

```
to complete

```odin
package main

import "core:fmt"
	

Age :: i16

Person :: struct {
  name : string,
  age : Age,
}

main :: proc() {

  p := Person {
      name = "odin",
      age = 10,
  }

  fmt.println(p)
}
// unions

```


# Enum

```go
type Choice int 
const (
    choice1 Choice = iota // start at 0 
    choice2 
    choice3 
)
```

```odin
Choice :: enum {
    Choice1 // start at 0 as well
    Choice2
    Choice3
}
```

# Variable

```go
// untyped string
const BLUE = "#0000FF"

// typed strings
const RED string = "#FF0000"

//regular variable
var yellow string 
yellow = "#FFFF00"

// syntax only work inside a function
// type is infered as well
green := "#00FF00"
```

```odin
// Constant 

// untyped string
BLUE :: "#0000FF"

RED : string : "#FF0000"

//regular variable
yellow : string // here yellow is declared
yellow = "#FFFF00"

// only inside procedure (aka function)
// type is infered
green := "#00FF00"
```



# Function


```go
func someFunction() int {}

func someFunction() (int,float32) {}

func someFunction(x  int8, y  int8) (int,float32) {}

// type grouping is valid
func someFunction(x , y : int8) (int,float32) {}

// named return parameters are possible in both language
func someFunction (x, y int8) (a int, b float32) {}

// method
func someMethod(s *Somestruct, x int){}
// method with sugar syntax 
func (s *Somestruct)someMethod(x int){}
```

In Odin function are called procedure and it is declared like so
```odin
// can as well have 1 or multiple return type 
some_procedure :: proc() -> i8 {}

some_procedure :: proc() -> (i8,f32) {}

some_procedure :: proc(x : i8, y : i8) -> (i8,f32) {}
// type grouping is valid
some_procedure :: proc(x,y: i8) -> (i8,f32) {}

some_procedure :: proc(x,y: i8) -> ( a i8, b f32) {}

// no method in odin, there bellow is just a procedure that accept a custom type 
some_procedure :: proc( cs : Customtype) {}
```


# if statement
if, else statement behave the same in both language 

# Loops 
Both language use `for` for looping with some key difference. 

```go
// range 
ODIN:
for i in 0..<3 {
    fmt.println(i)
}

GO:
for i := range 3 {
    fmt.Println(i)
}

arr := [3]int{1,2,3}

// index come first in golang
for i,v := range arr {
    v *= 2 // this will failed because golang provide the copy
    arr[i] *= 2 // this will succeed
}


ODIN:
// value come first
for &v,i in arr {
    // to change the value we need to make v adressable 
    v^ *= 2 //deference it and change it 
}

```
// to do
# switch 




