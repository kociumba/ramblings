---
publish: "true"
created: 2026-06-23T16:04:30.120Z
modified: 2026-10-28T22:42:18.000Z
published: 2026-10-28T22:42:18.000Z
topic difficulty: beginner
"\n> [!tip]\n> It is often conventional to name constant using UPPERCASE names, though this is ultimately up to your preference\n\n```cpp\n// c/c++\nconst int FOO = 69;      // portable across c and c++\nconstexpr int FOO = 69;  // c++11 and up\ \n```\n\n```go\n// go\nconst FOO int = 69\n```\n\n```odin\n// odin\nFOO ": "69"
---

Variables are a _named instance of a [[types|type]]_:

```cpp
// c/c++
int foo = 69;
```

```go
// go
var foo int = 69
```

```odin
// odin
var foo: type = 69
```

```rust
// rust
let mut foo: i32 = 69;
```

> [!hint]
> A variable is nothing without a [[types|type]]

Many languages can also perform _type deduction_ for you when creating a variable:

```cpp
// c++11 and up
auto foo = 69;  // inferred to be int
```

```go
// go
foo := 69  // inferred to be int
```

```odin
// odin
foo := 69  // inferred to be int
```

```rust
// rust
let mut foo = 69;  // inferred to be i32
```

A variable like this can be:

- reassigned: `foo := 69; foo = 420` this simply overwrites the value of the variable
- compared: `foo, bar := 69, 420; foo == bar` this gives us a [[types#^booleans|boolean]] value of `true` if the values are the same or `false` if they are not. This will be very useful in [[control flow]]

### constant variables ? - constants

Yes the naming is idiotic an "unchanging changeable" but their purpose and working principle are fully summed up in that

A constant is like a variable a named instance of a type **that <u>can not</u> change it's value**

These are typically used for example for defining specific so called _magic numbers_ for example the value of $\pi$ is often hardcoded using a constant: `const PI = 3.14159;`

> [!tip]
> It is often conventional to name constant using UPPERCASE names, though this is ultimately up to your preference

```cpp
// c/c++
const int FOO = 69;      // portable across c and c++
constexpr int FOO = 69;  // c++11 and up 
```

```go
// go
const FOO int = 69
```

```odin
// odin
FOO :: 69
```

```rust
// rust
const FOO: i32 = 69;
```

### the secret third kind - immutable variables

For a long time these were used interchangeably with constants, both things meant the same concept

But with the rise of _compile time_ in newer languages these two slightly differentiated:

- immutable variable - is an unchanging variable, which to the computer looks like a normal variable:

```rust
// rust
let foo = 69;      // immutable - cannot be reassigned
let mut bar = 69;  // mutable - can be reassigned with `bar = 420;`
```

> [!hint]
> Despite many other languages supporting immutability in the c-style family of languages rust is one of the only ones from this family to have immutability by default

- constants - are now typically understood as variables _resolved at compile time_, meaning their value is literally contained in the final program and you can simply access it via the name give to it

### a curious lack of value

Most languages let you define variables without immediately assigning values to them

```cpp
// c/c++
int foo = 69;
```

```go
// go
var foo int = 69
```

Depending on the language this can produce different results

Some languages like c and c++ will simply use the _uninitialized memory_ and the variable will hold a garbage value from whatever was previously stored in that place in memory

Newer languages like go or odin, java or kotlin will use 1 of 2 solutions to this problem:

- all [[types]] will have a `null` or `nil` value which is automatically assigned to them and signifies a lack of value
- all [[types]] will have a default "zero" value which is automatically assigned to them and is simply the `0` of that type e.g. `int` would be `0`, `string` would be `""`, `bool` would be `false` and so on

Generally speaking the _default zero value_ approach is simpler to reason about, but languages that use the _null or nil_ values are typically also higher level and as such they offer nicer syntax and many different utilities that simplify your work
