---
publish: "true"
created: 2026-06-23T11:34:21.000Z
modified: 2026-10-28T22:41:30.000Z
published: 2026-10-28T22:41:30.000Z
topic difficulty: beginner
"\n```cpp\n// c/c++\nint add(int a, int b) {\n\treturn a + b;\n}\n```\n\n```go\n// go\nfunc add(a int, b int) int {\n\treturn a + b\n}\n```\n\n```odin\n// odin\nadd ": "proc(a: int, b: int) -> int {"
"\n```cpp\n// c/c++\nvoid do_something() {...}\n```\n\n```go\n// go\nfunc add() {...}\n```\n\n```odin\n// odin\nadd ": proc() {...}
---

Functions (also known as procedures, methods, closures and a few more), all these names technically have slightly different meanings but they all refer to the same basic concept:

> [!important]
> **A reusable piece of code**, which has a defined behavior and can be called with different parameters

Examples of simple functions performing integer addition in a few different languages:

```cpp
// c/c++
int add(int a, int b) {
	return a + b;
}
```

```go
// go
func add(a int, b int) int {
	return a + b
}
```

```odin
// odin
add :: proc(a: int, b: int) -> int {
	return a + b
}
```

```rust
// rust
fn add(a: i32, b: i32) -> i32 {
	return a + b;
}
```

In each of these languages this function can then be called like so:

> [!hint]
> A _function call_ is an invocation of that function, or in plain terms it's using the function, making it run

```cpp
add(69, 420); // the ; can be ommited in some languages
```

As you can see the pattern is the same in each language despite some syntactical differences

Every function has:

- a name: `add` - which is used to call it, and refer to it
- parameters that it can take: `(int a, int b)` - these act like [[basics/variables|variables]] inside that function and have specific [[types]]
- the scope: `{...}` - is the body of the function where is behavior is defined
- return type: `-> int` - defines what the function will return to it's caller and requires a specific [[types|type(s)]]

#### what if no return type ?

In virtually any language a function can simply return nothing, if all it performs is some _side effects_, then there is no point in returning anything most of the time:

```cpp
// c/c++
void do_something() {...}
```

```go
// go
func add() {...}
```

```odin
// odin
add :: proc() {...}
```

```rust
// rust
fn add() -> () {...}
```

> [!hint]
> Before continuing this topic I would strongly recommend reading about [[variables]] if you don't know what they are

### blasphemy - impure functions

The functions shown above, are _pure_. This is a term from functional programming which is modeled closely after mathematical concepts

> [!example]- extra info
> _Pure_ functions are essentially a direct translation of the mathematical concept of a function (or mapping): $f : X \to Y$ - each input has exactly 1 predictable output.
> To learn more about functional programming and concepts I recommend reading about it [here](https://brilliant.org/wiki/lambda-calculus/), unfortunately to dive deeper into this subject you will need to sift through academic lectures since that is where most info about it lies

_Purity_ here means the functions only perform an operation of the parameters given to them, and nothing else

In normal programs you will most likely want your functions to do more. After all a full program rarely runs only on functions

This is where we need functions that perform _side effects_. A _side effect_ here being causing any state outside of the function itself to change, for example the infamous "Hello World!":

```c
#include <stdio.h>

int main() {
	printf("Hello World!\n");
}
```

By definition this is an _impure_ function since as a _side effect_ it causes the state of the terminal to change, by printing "Hello World!"

> [!important]
> As you might have guessed, very few real programs can function using only _pure_ functions, and even functional languages like [Haskell](https://www.haskell.org/) require ways of allowing _impurity_

### localized sin - scopes

Most things in programming are enclosed by something we refer to as a _scope_ also referred to as: body, block or context

This serves many purposes, but probably the most important is that it divides the program into segments, so that you can for example reuse names, or limit the visibility of certain things

```cpp
#include <stdio.h>

int foo = 69;                    // variable in global scope

int add(int a, int b) {          // opening scope of function 'add' 

	int bar = 420;              // variable in scope of function 'add'
	
	return a + b;
}                               // closing scope of function 'add'

int main() {                    // opening scope of function 'main'

	printf("foo: %d\n", foo);  // variable from encapsulating scope, is available
	
	printf("bar: %d\n", bar);  // variable from a different scope, is unavailable

}                               // closing scope of function 'main'
```

This example shows how _scopes_ limit the reach reach of definitions and things like variables, more importantly this **will <u>not</u> compile**, the compiler will throw an error about accessing a variable that is not present in the `main` function scope

> [!important]
> Scopes behave like a tree, **anything on a branch can see what's below it on the same branch, but not what is on other branches**

The 2 functions _scopes_ in the example above are on the same level, they both branch of the _global scope_ which means they are like 2 different branches and they can not access what is defined in the other one

This way of organizing code may seem weird: "Why limit what we can use? Why not just have access to everything?"

This would certainly make simple programs simpler to reason about, but once you get into any kind of complexity, that approach would run into a few issues:

1. memory - computers have limited memory and they can not keep everything in it at all times, the design of _scopes_ allows computers to only keep certain things in memory for the duration of that scope, this is called a _lifetime_ ^scope-memory-management
2. name pollution - if everything would be accessible from anywhere, you would have to have a unique name for everything you create. In programs that define thousands of different variables, types, functions and so on this would be a real issue

### how to use functions ?

We have covered the different types of functions, how to define them and and what they are, but how do you use them ?

Well the answer is simpler than you might expect, **all you can really do is call functions**

Yes that is right, any program can be built by simply defining a set of functions and making them call each other in the correct order and conditions

Consider this example (since this is real code you should also read about [[control flow]] to understand it):

```c
#include <stdio.h>

int fibonacci(int n) {
    if (n == 0) {
        return 0;
    } else if (n == 1) {
        return 1;
    }
    
    return fibonacci(n - 1) + fibonacci(n - 2);
}

int main() {
    int term = 6;
    
    printf("The %d fibonacci number is %d\n", term, fibonacci(term));
    
    return 0;
}
```

^fibonacci-example

This example code will calculate [Fibonacci sequence](https://www.mathsisfun.com/numbers/fibonacci-sequence.html), this programming example is a cliché by now, but it illustrates a few different important principles:

1. you can actually see functions at work here, they perform real work
2. recursion - which will be the topic of the next chapter

### oops stack overflow - recursion

_Recursion_ gained an almost mythical status of this unexplained, cryptic boogieman among programming students

In reality _recursion_ is so simple you might have stumbled onto it on your own and not even realize

> [!important]
> A _recursive_ function is a **function that calls itself**, it is essentially a functional alternative to the concept of _loops_ which we talk about in [[control flow]]

Imagine a robot that can assemble another robot just like itself, that would be recursion

In real programs recursion often happens in 2 or more steps rather than exactly 1 function calling itself, for example function `a` calls function `b` then function `b` calls function `a` and so on

Where is the _recursion_ in that [[#^fibonacci-example]] from earlier ?

```c
return fibonacci(n - 1) + fibonacci(n - 2);  // <-- here
```

"Each number in the Fibonacci sequence are 2 previous numbers from the sequence added together", this code does exactly that:

- what is `fibonacci(6)`: `fibonacci(5) + fibonacci(4)`
  - what is `fibonacci(5)`: `fibonacci(4) + fibonacci(3)`
    - what is `fibonacci(4)`: `fibonacci(3) + fibonacci(2)`
      - ...

If you are inclined to logical thinking you might be saying that this looks quite inefficient, and to that i have to say _it very much is_

Just so happens that computers are very powerful these days and this code can run it's inefficient calculation at a satisfying speed up until large `n` values, but if you were to set `n = 100000000` this would most likely crash with a `stack overflow` error which in c would be the infamous `segmentation fault`

The explanation of what is a `stack` and what is a `heap` will be saved for later, but this goes back to this issue [[#^scope-memory-management]], since the _scopes_ of the functions aren't closed before we run the function again, their memory footprint accumulates, and causes the program to crash if not managed correctly
