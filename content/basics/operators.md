---
publish: "true"
created: 2026-06-25T13:19:54.960Z
modified: 2026-10-28T22:42:06.000Z
published: 2026-10-28T22:42:06.000Z
topic difficulty: beginner
---

When programming we need to perform actions, like assign _values_ to [[variables]] or comparing _values_ of [[variables]] to see if they are equal

All of this is covered by _operators_, most real work is done with them

> [!important]
> _Operators_ are special symbols that perform specific actions on the data in your program

---

There is an important concept connected to _operators_:

- _left side values_ aka. _lvalues_
- _right side values_ aka. _rvalues_

These refer to what is on the _left_ and _right_ of an operator, in some cases the behavior of the operator will be dependent on what is the _lvalue_ and what is the _rvalue_

Due to this, for the rest of this document we will refer to these as their short names: _lvalue_ and _rvalue_

There is also something called _unary operators_ this is a specific set of operators that only take an _rvalue_ e.g. `!a`, this will be discussed further when they come up

---

A use of an operator like `a + b` is called an _expression_ and is seen by the language as a _value_, so writing `69 + 420` is the same for the language a writing `489`

> [!important]
> _Expressions_ are any piece of code which can evaluate to a single _value_

For this reason calling a [[functions|function]] that returns a value IS an _expression_, the same thing is true for [[variables]] since they hold a _value_ they can be treated as that _value_ thus allowing them to be treated as an _expression_

### back in math class - arithmetic operators

First type of operators is _arithmetic operators_, they are straight up borrowed from math, and perform the same functions as in math

| _operator_ | it's function                                                  | example | notes                                                              |
| ---------- | -------------------------------------------------------------- | ------- | ------------------------------------------------------------------ |
| `+`        | performs addition of _lvalue_ and _rvalue_                     | `a + b` |                                                                    |
| `-`        | performs subtraction of the _rvalue_ from the _lvalue_         | `a - b` |                                                                    |
| `*`        | performs multiplication of _lvalue_ and _rvalue_               | `a * b` |                                                                    |
| `/`        | performs division of _lvalue_ by _rvalue_                      | `a / b` | if performed on integer [[types]] will discard the fractional part |
| `%`        | returns the remainder of _lvalue_ divided by _rvalue_ (modulo) | `a % b` | typically only works on integer [[types]]                          |

#### almost math

There are 2 operators which allow for incrementing or decrementing a numeric value by 1, each time they are used

| _operator_ | it's function                      | example | notes                                                           |
| ---------- | ---------------------------------- | ------- | --------------------------------------------------------------- |
| `++`       | increments the given _lvalue_ by 1 | `a++`   | is a special case _unary operator_ which takes only an _lvalue_ |
| `--`       | decrements the given _lvalue_ by 1 | `a--`   | is a special case _unary operator_ which takes only an _lvalue_ |

> [!example]- extra info
> C and C++ are unique languages that allow using this also as normal _unary operators_ - as prefixes: `++a` they technically have some special semantic differences but, it's rarely used and often makes the code less readable since everyone will be used to `a++` outside of those 2 specific languages

#### chimaera of math and programming - comparison and assignment

There are a few operators which perform functions very similar to what you might find in math but are going to be slightly different in programming

Mainly you will have to watch out for `=` and `==` since believe it or not they are different AND different than their math counterparts

| _operator_ | it's function                                                           | example  | notes                                                                                                                                  |
| ---------- | ----------------------------------------------------------------------- | -------- | -------------------------------------------------------------------------------------------------------------------------------------- |
| `=`        | assigns the _rvalue_ to the _lvalue_                                    | `a = b`  | this requires _lvalue_ to be something that can actually hold a value (NOT an _expression_) like for example a [[variables\|variable]] |
| `==`       | compares the _lvalue_ to the _rvalue_                                   | `a == b` | this evaluates to a [[types#^booleans\|boolean]] value of `true` or `false` and is commonly used in [[control flow]]                   |
| `<=`       | returns `true` if the _lvalue_ is less than or equal to the _rvalue_    | `a <= b` |                                                                                                                                        |
| `>=`       | returns `true` if the _lvalue_ is greater than or equal to the _rvalue_ | `a >= b` |                                                                                                                                        |
| `<`        | returns `true` if the _lvalue_ is strictly less than the _rvalue_       | `a < b`  |                                                                                                                                        |
| `>`        | returns `true` if the _lvalue_ is strictly greater than the _rvalue_    | `a > b`  |                                                                                                                                        |
| `!=`       | returns `true` if the _lvalue_ is not equal to the _rvalue_             | `a != b` |                                                                                                                                        |

#### shorthand assignments

To make certain code simpler to write there are so called _compound assignment operators_ which are simply combining the assignment `=` with another operation

| _operator_ | it's function                                        | example  | equivalent to |
| ---------- | ---------------------------------------------------- | -------- | ------------- |
| `+=`       | adds _rvalue_ to _lvalue_ and assigns result         | `a += b` | `a = a + b`   |
| `-=`       | subtracts _rvalue_ from _lvalue_ and assigns result  | `a -= b` | `a = a - b`   |
| `*=`       | multiplies _lvalue_ by _rvalue_ and assigns result   | `a *= b` | `a = a * b`   |
| `/=`       | divides _lvalue_ by _rvalue_ and assigns result      | `a /= b` | `a = a / b`   |
| `%=`       | assigns remainder of _lvalue_ / _rvalue_ to _lvalue_ | `a %= b` | `a = a % b`   |
Notice how `a += 1` is the same as `a++`, this is relevant since some languages don't implement  `++` and you sometimes might need to supplement it with `+= 1`

### this makes no sense - logical operators

The category of operators which is only really seen in programming is _logical operators_, but these will be familiar to you if you have ever learned about [Boolean Algebra](https://en.wikipedia.org/wiki/Boolean_algebra)

All of these operate on [[types#^booleans]], since there surprisingly a lot you can actually do with something that can only have 2 values

| _operator_                | it's function                                                   | example                       | notes                                                                                  |
| ------------------------- | --------------------------------------------------------------- | ----------------------------- | -------------------------------------------------------------------------------------- |
| `&&`                      | returns `true` if both the _lvalue_ AND the _rvalue_ are `true` | `a && b`                      | also known as _logical AND_, if the _lvalue_ is `false` the _rvalue_ is not evaluated  |
| <code>||</code> | returns `true` if either the _lvalue_ OR the _rvalue_ is `true` | <code>a || b</code> | also known as _logical OR_, if the _lvalue_ is `true` the _rvalue_ is not evaluated    |
| `!`                       | returns the opposite boolean value of the _rvalue_              | `!a`                          | also known as _logical NOT_, this is a unary operator — it only takes a single operand |

#### 0xDEADBEEF - bitwise operators

> [!warning]
>
> ### Feel free to skip this topic for now!
>
> _Bitwise operators_ while powerful and useful, are quite complicated and you probably won't need to use them at the beginning

These operators are very similar to _logical operators_ but they work on the base2 representation of other data

> [!important]
> _Bitwise operators_ allow you to perform base2 mathematical operations on arbitrary data, which most of the time won't be interpreted as base2

| _operator_      | it's function                                       | example             | notes                                                                                                    |
| --------------- | --------------------------------------------------- | ------------------- | -------------------------------------------------------------------------------------------------------- |
| `&`             | performs bitwise AND on _lvalue_ and _rvalue_       | `a & b`             | each bit is set to `1` only if both corresponding bits are `1`                                           |
| <code>|</code> | performs bitwise OR on _lvalue_ and _rvalue_        | <code>a | b</code> | each bit is set to `1` if either corresponding bit is `1`                                                |
| `^`             | performs bitwise XOR on _lvalue_ and _rvalue_       | `a ^ b`             | each bit is set to `1` if the corresponding bits are different                                           |
| `~`             | inverts all bits of the _rvalue_                    | `~a`                | unary operator — flips every `0` to `1` and every `1` to `0`                                             |
| `<<`            | shifts bits of _lvalue_ left by _rvalue_ positions  | `a << b`            | equivalent to multiplying by 2<sup>_rvalue_</sup>; bits shifted in are `0`                               |
| `>>`            | shifts bits of _lvalue_ right by _rvalue_ positions | `a >> b`            | equivalent to integer division by 2<sup>_rvalue_</sup>; behavior on the sign bit depends on the language |

> [!note]+
> If you recall the _compound assignment operators_ from earlier, the same can be done with _bitwise operators_, so you can use operators like: `|=`, `&=`, `^=`, `<<=`, `>>=`
> Since they all follow the same pattern and work in the same way, where `a |= b` is the same as `a = a | b`

As a usage example `|` is often used to encode multiple config options into a single integer value

This is done by setting the config options to specific values such that they are powers of 2 (this makes it so that every value uses only 1 of the bits of the integer), then their values can be combined together into a single integer value and retrieved as singular options

This example was inspired by the amazing library [Raylib](https://github.com/raysan5/raylib):

```c
#include <stdio.h>
#include <stdbool.h>

// flags are set so that each flag occupies a different bit
//
// this is done using bit shifting with <<
typedef enum {
    FLAG_FULLSCREEN_MODE    = 1 << 0,  // 1   
    FLAG_WINDOW_RESIZABLE   = 1 << 1,  // 2
    FLAG_VSYNC_HINT         = 1 << 2   // 4     
} ConfigFlags;

void InitWindow(int width, int height, const char *title, unsigned int flags) {
    printf("Initializing %dx%d window: \"%s\"\n", width, height, title);
    printf("Raw flags integer value: %u\n\n", flags);

    // each flag can be extracted from the combined value using &
    if (flags & FLAG_FULLSCREEN_MODE) {
        printf("[Window] Starting in Fullscreen mode.\n");
    } else {
        printf("[Window] Starting in Windowed mode.\n");
    }

    if (flags & FLAG_WINDOW_RESIZABLE) {
        printf("[Window] Resizing enabled.\n");
    }

    if (flags & FLAG_VSYNC_HINT) {
        printf("[Render] VSync hint enabled.\n");
    }
}

int main(void) {
    // these specifically defined flags can be combined into a single integer value 
    unsigned int window_config = FLAG_VSYNC_HINT | FLAG_WINDOW_RESIZABLE | FLAG_FULLSCREEN_MODE;

    InitWindow(800, 600, "example", window_config);

    return 0;
}
```
