---
publish: "true"
created: 2026-06-23T13:10:48.930Z
modified: 2026-10-28T22:42:12.000Z
published: 2026-10-28T22:42:12.000Z
topic difficulty: beginner
---

Types in programming essentially serve as shapes, since the computer needs to know what shape of data to expect

Most languages will have 2 classes of types:

- language defined primitive types - these will commonly include: integer types of different bit widths, floating point types, booleans and more recently strings
- user defined types - these are defined by the user in the program and they will commonly include: structure/class types, enumerators and union types

> [!hint]
> A type is nothing without a [[basics/variables|variable]]

### primitive types

a generic list of primitive types would look something like this (this is a list of go primitive types since that language has the smallest and simplest list):

```go
bool

string

int  int8  int16  int32  int64
uint uint8 uint16 uint32 uint64 uintptr

byte // alias for uint8

rune // alias for int32
     // represents a Unicode code point

float32 float64

complex64 complex128
```

- `bool` types - represent a `true` or `false` value, essentially a `1` or `0` (note they are typically not actually represented in memory as 1 bit, typically they take up a whole byte so 8 bits) ^booleans
- `string` types - represent text, or more specifically a sequence of characters, which are just numbers to the computer
- `int` types - represent integer numbers, the `8`,  `16`, `32` and `64` suffixes describe how many bits this number uses, which translates to the maximum value it can represent, the `u` prefix signifies the number is _unsigned_ which means the first bit of it is not used to represent whether it's negative or not, this means the number can not be negative but has a higher max value
- `float` types - represent floating point numbers, the `32` and `64` suffixes work the same as in `int` types

`byte` and `rune` have comments explaining what they are and `complex` numbers are available only in newer languages and those more oriented towards game/graphical programming, they represent [mathematical complex numbers which you can read more about here](https://www.mathsisfun.com/numbers/complex-numbers.html)

#### primitive types 2$^\textsf{tm}$ - collections

Most languages support a few kinds of "collection" types which are the middle ground between [[#primitive types]] and [[#user defined types]], the most common one are `arrays`, and in newer languages you can find `slices` and `lists`

These types occupy the middle ground since they behave more like modifiers to other types instead of types on their own, for example this is how you would define an `array` of `int` types, meaning this will hold multiple `int` types in a series with unique index values which refer to their place in the `array`:

```c
// c/c++
int foo[3] = {69, 420, 2137};
```

```go
// go
var foo [3]int = [3]int{69, 420, 2137}
```

```rust
// rust
let foo: [i32; 3] = [69, 420, 2137];
```

```odin
// odin
foo: [3]int = {69, 420, 2137}
```

As you can see in the languages we use as examples `arrays` have a **fixed capacity** this is due to how memory works and is outside the scope of this overview

But most of the time you will want to be able to dynamically grow and shrink the array, which is supported by most modern languages:

```go
// go
bar := []int{69, 420}
bar = append(bar, 2137)
```

```odin
// odin
bar: [dynamic]int
append(&bar, 69)
```

I will spare the rust and c++ examples since they can get very verbose and complex, good news is that in higher level languages the basic arrays are typically dynamic, so you won't have to do any extra work in python, javascript or lua

> [!example]- extra info
> The D language has an interesting oddity, it supports something called `associative arrays`:
>
> ```d
> int[string] foo;
> foo["bar"] = 69;
> ```
>
> These are functionally identical to a concept that is called a `map` in other languages, and in that form is supported by most other languages. **A `map` is an `array` where indices are a <u>not</u> numbers**

### user defined types

For the user defined types examples we will use Rust since go is too simplistic to cover all 3 most common user defined types:

```rust
struct Foo {
	field1: type1,
	field2: type2,
	...
}

enum Bar {
	Value1,
	Value2,
	...
}

union Baz {
	field1: type1,
	field2: type2
	...
}
```

- `struct` types - represent structures of data, notice that all fields need their own type as well, which means a structure is simply a grouping of variables under a common name and lifetime
- `enum` types - represent enumerations, in this example `Value1` would get the value of `0` and `Value2` the value of `1` (since in programming we start counting from 0). An enum like this allows for representing options or config values with a name, instead of simply their underlaying number ^enums
- `union` types - will often look the same as struct types, but they have a fundamentally different job, they represent a state where the union holds _only 1 of the types in it at a time_. This is used for situations where an outcome of some operation can produce one type of data _or_ another type of data but never both

> [!info]
> you will not use unions too often, in fact older languages don't even support them in he same way newer ones do

### what do if types don't match ???

> [!hint]
> It is highly recommended to read about [[variables]] if you don't know what they are before reading this part

This question will come up often when programming let's take this hypothetical:

```rust
// rust
fn main() {
    let foo: i32 = 69;
    let bar: f32 = 420.0;
    let baz: i32 = foo + bar;  // ERROR: no implementation for `i32 + f32`
}
```

That example will fail with an error like so:

```
error[E0277]: cannot add `f32` to `i32`
  --> src/main.rs:3:21
   |
3  |     let baz = foo + bar;
   |                     ^^^ no implementation for `i32 + f32`
   |
   = help: the trait `Add<f32>` is not implemented for `i32`
```

In this situation we will need to _cast_ the variable to a matching type.

Different languages have different types of _casts_, but the idea remains the same **a cast coerces a value of one type into another type**

Some languages are also more permissive, in c/c++ the same operation would convert the `float` into and `int` automatically and added them together only emitting a warning about _implicit type conversion_

So the solution to our hypothetical in rust would be:

```rust
let baz = foo + bar as i32; // this casts bar from f32 into i32
```

In some other languages this might look like this:

```cpp
// c/c++
int baz = foo + (int)bar;               // C-style cast
int baz = foo + static_cast<int>(bar);  // C++ cast
```

```go
var baz int32 = foo + int32(bar)
```

```odin
baz: i32 = foo + i32(bar)
```

> [!important]
> Remember that while you can convert between types, the conversions are not _lossless_, since `f32` can represent decimal places of a number and `i32` can not, the bits carrying that data will be lost in the conversion, **keep this in mind for any and all casts**
