---
publish: "true"
created: 2026-06-25T12:37:33.040Z
modified: 2026-10-29T10:59:48.000Z
published: 2026-10-29T10:59:48.000Z
topic difficulty: beginner
---

So you want to write a program?

Well the first thing you will need is a _programming language_, there are way too many to choose from

> [!note]
> This series has to assume you posses some basic knowledge about computers already, thanks to this it can stay a series of articles rather than a full length book

Here we will be focusing on _compiled_ languages like: [c](https://en.wikipedia.org/wiki/C_\(programming_language\)), [c++](https://en.wikipedia.org/wiki/C%2B%2B), [odin](https://odin-lang.org/), [zig](https://ziglang.org/), [go](https://go.dev/), or [rust](https://rust-lang.org/)

In my honest opinion you should not start with [rust](https://rust-lang.org/), [zig](https://ziglang.org/) or [c++](https://en.wikipedia.org/wiki/C%2B%2B), they **will** be too overwhelming

You should learn programming in [c](https://en.wikipedia.org/wiki/C_\(programming_language\)), but maybe not necessarily try to program a complex program like for e.g. a game

This narrows my initial recommendations to [go](https://go.dev/) or [odin](https://odin-lang.org/), but really pick whatever ends up looking fun

> [!example]- extra info
> You could always write c++ and simply use it like c with extra features (my preferred style), but this will be hard in the beginning and you will have to do everything differently than any tutorials or guides will tell you
> I only recommend this is you have a _strong grasp of the fundamentals of programming_

### ancient rune magic - compiler

The first thing you will notice that all these languages have _compilers_

> [!important]
> A compiler is a very complicated program, but all you need to know for now is that _**a compiler is the thing that will take the code you write and translate it into something a computer can execute**_

This process is called _compilation_ and produces an _executable file_

If you use windows you will be familiar with them as they have the well known `.exe` file extension, on linux and macos _executable files_ will have no file extension

So to get started you will need to go to your chosen languages website and acquire it's compiler, preferably the newest available version

> [!example]- extra info for c/c++
> If you picked c or c++ getting a compiler will be somewhat harder, since there are a few competing standards, and neither one works on all operating systems (at least natively)
>
> - on windows you will need [msvc](https://visualstudio.microsoft.com/vs/features/cplusplus/) or [visual studio](https://visualstudio.microsoft.com/) or [wsl](https://learn.microsoft.com/en-us/windows/wsl/install) (if using wsl refer to the linux point)
> - on macos you will typically need [xcode](https://developer.apple.com/xcode/) or a custom [clang](https://clang.llvm.org/)installation
> - on linux you can install [gcc](https://gcc.gnu.org/) or [clang](https://clang.llvm.org/)

### I didn't know this was a writing class - source files

Great we have a _compiler_ but nothing to _compile_ this is where we need to write _source code_ in _source files_

> [!important]
> A _source file_ is simply a text file containing code in a specific language, they need to use the language specific file extension

So for languages I presented earlier you would write code in:

- `.c/.h` - files for c
- `.cpp/.hpp/.h` - files for c++
- `.odin` - files for odin
- `.zig` -files for zig
- `.go` -files for go
- `.rs` - files for rust

Typically your program will start in a `main.[lang extension]`, though some languages deviate from this

If they do this information will be present on the language website 99% of the time

### how does this thing work ?

Before we start learning how to actually program, we need to cover some basic properties of code that lay the foundation for everything to come

> [!important]
> _**Code is executed line by line from the top downwards**_

Now this is both true and false, code _IS_ executed this way, _BUT_ execution can jump to a different place in the file

This continues on executing line by line downward but simply isn't always _linear_

Another basic principle is that you program needs to start somewhere, this magical starting place is typically a `main` [[functions|function]] - you will read about [[functions]] in a second

You can think of it as the place in your program where the operating system will start executing it (huge simplification)

This is also the reason why execution needs to be able to jump around, since otherwise we would need to write everything inside the `main` [[functions|function]] rather than in pieces

### humble beginnings - start writing code

Now before we actually start writing code you will need to learn about some basic concepts in programming, so you will have to do some light reading

This order is generally going to ensure you understand as much as possible of what's written, there are many links and references in each article, so feel free to jump around. Just try to stay on track with this thorough line:

1. [[code comments]] - while not strictly necessary, you will probably want to know what they are
2. [[variables]] and [[types]] - you can almost treat these 2 articles as 1, their topics and explanations are very tightly coupled, and make up the core knowledge, everything will build on
3. [[operators]] - will clear up some questions that might come up after the last 2, and presents a few more core ideas
4. [[functions]] - familiarizes you with the foundational building blocks of programs
5. [[control flow]] - covers how those blocks can actually perform operations
6. [[naming]] - introduces some industry standards and helpful tips for actually writing your own code

If you followed this list and read all the articles _**good job!**_

You should be ready to write your first piece of code with confidence

> Be prepared for some googling and research since i can't cover literally everything needed here, mainly your languages standard library

To clarify a standard library is the set of functionality a language provides out of the box

I will give you a task and an example solution to it here, so that you can practice yourself:

> [!info]
> In your chosen language write a terminal program that asks the user to guess a number between 0 and 100, each time picking a random number, then sum up the number of correct guesses and display it

> [!example]- spoiler: solution
> The example implementation i will be showing here is going to be in c, since that is the simplest language we covered
>
> Everything here is replicable in other languages, and if you were paying attention when reading the previous articles you should be able to translate this example into other languages
>
> ```c
> #define _CRT_SECURE_NO_WARNINGS
>
> #include <stdio.h>
> #include <stdlib.h>
> #include <time.h>
>
> // define the number of rounds to play
> #define ROUNDS 3
>
> // returns a random number in range from lower to upper
> int get_random_in_range(int lower, int upper) {
>     return lower + rand() % (upper - lower + 1);
> }
>
> // this is where the program will begin
> int main() {
>     int score = 0;
>     srand(time(NULL));  // seed the random number generator
>
> 	 // loop for the defined number of rounds
> 	 for (int i = 0; i < ROUNDS; i++) {
>         int guess = 0;
>         printf("enter your guess: ");
>         scanf("%d", &guess);  // get user input
>
> 	    int target = get_random_in_range(0, 100);
> 	    if (guess == target) {
> 			printf("correct\n");
> 			score++;  // add score if guessed correctly
>       } else {
>           printf("wrong the number was: %d\n", target);
>       }
>    }
>
>     if (score == 0) {
>         printf("you have not guessed any of the numbers correctly");
>         return 0;
>     }
>
> 	if (score > 0 && score < ROUNDS) {
>         printf("you have guessed %d numbers correctly", score);
>         return 0;
>     }
>
>     // early returns above allow use to be certain
>     // that this will only execute when all guesses were correct
>     printf("it's not good to cheat you know");
> }
> ```
>
> To calm anyone looking at this and seeing things they don't know:
>
> - `#define _CRT_SECURE_NO_WARNINGS` - is needed to silence compiler warnings about using the `scanf` [[functions|function]] on windows
>
> - `#define` - serves as a special way to create [[variables#constant variables ? - constants|constants]] in c and c++
>
> - `#include` - is the way you include external code in your program in c and c++, here we include parts of the standard library which are always available
>
> > [!warning]
> > This example is not _safe_, we for example don't check if `scanf` failed which could cause issues in a real program

When writing your code try not to mindlessly copy and paste from the internet or ai, while i don't deny those tools usefulness (like many teachers would do), unfortunately I do have to warn you about becoming _complacent_

On the topic of ai, ai _WAS_ used in the making of this guide, but it was used in the same way i would recommend you use it: _as a tool_ (here specifically mostly for speeding up looking things up). Don't blindly trust anything ai says or copy paste from it without understanding, and I know it's easy to forget about this so _hold yourself accountable_

The same goes for agents which are getting more popular recently, it might be really alluring to create a complex app in a fraction of the time it would normally take and without exerting a lot of effort, but agents have many hidden limitations that make this a short sighted pursuit:

- your financial limitations since agents get pretty expensive
- code quality, code produced by ai is only slightly above average level when it comes to the best models, they don't do things like abstract away common functionality or remember to use what they abstracted
- you don't know what the code produced actually does therefore you can  not explain it nor can you easily modify it yourself, this causes an issue where ai code often will only ever be edited by ai, since reading it and understanding enough to modify it is a demanding task

Now if you don't have any ideas what program to write on your own, you can move onto: [[your first game]] (when it's finished)
