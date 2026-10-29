---
publish: "true"
created: 2026-06-24T11:39:39.480Z
modified: 2026-10-28T22:41:22.000Z
published: 2026-10-28T22:41:22.000Z
topic difficulty: beginner
---

Great so now you can write [[functions]] and [[variables]] and you know what [[types]] are, but how do you actually control what your program does ?

These examples will mostly utilize c/c++, this is because these will be a little longer than the examples before. The concepts are the same in most other languages, there are simply some syntactical differences

### the humble if statements

`if` statements are the backbone of most programs, the simple ability to decide if a part of the code executes or not, provides the foundational building blocks for any program

```cpp
if (condition) {
	printf("condition was true\n");
} else if (condition2) {
	printf("condition2 was true\n");
} else {
	printf("condition2 was false\n");
}
```

As you can see the idea is very simple, in fact it basically reads like English

> [!important]
> `if` statements only execute the code in their [[functions#localized sin - scopes|scope]] <u>if</u> the condition it is given is equal to the [[types#^booleans|boolean]] value of `true`.
> This can be followed up with `else` which executes it's scope if the original condition equals to `false`, or `else if (condition)` which let's you check another condition

Each of these [[functions#localized sin - scopes|scopes]] created by these comparisons is called a _branch_, which means an `if` statement _branches_ out the code

> [!example]- extra info
> Modern CPUs actually have a special unit called a _branch predictor_ which is supposed to predict which `if` statement branches are going to be taken by the running program and preload resources associated with them

### time to write a game - loops

The more practical alternative to [[functions#oops stack overflow - recursion|recursion]] are loops, they come in many flavors in different languages

In c++ alone we have these kinds of loops:

```cpp
while (condition) {
	...
}

do {  // barely ever used
	...
} while (condition);

for (variable_initialization; condition; update) {
	...
}
```

Now these are only outlines of how these loops work, so let's see some specific examples of how they may be used:

```cpp
int count = 1; 
while (count <= 3) { 
	printf("count: %d", count); 
	count++;
}
```

```cpp
int count = 1; 
do { 
	printf("count: %d", count); 
	count++;
} while (count <= 3);
```

```cpp
for (int i = 1; i <= 3; i++) { 
	printf("i: %d", i); 
}
```

The `for` loop is probably looking the scariest here, but it is the most commonly used by far, this is due to it's self contained nature, as you can see the variable used to keep track of repetitions is defined inside the loop itself, which if you remember [[functions#localized sin - scopes|scopes]], means that it does not leak outside of the loop

Hence `while` loops are essentially _the manual loop mode_, and they let you do silly things like:

```cpp
while (true) {
	...
}
```

Which as you might expect will just loop forever and hang, but this is where the second most important concept in loops comes in: the `break` and `continue` statements:

```cpp
int count = 1;

while (true) {
	count++;
	if (count >= 3) {
		break;
	} else {
		continue;
	}
} 
```

Now we are really _driving the metaphorical manual of loops_, this example is really simple but this is the basic principle of how _games_ and _graphical applications_ work

> [!important]
>
> - `break`: completely exits the loop and moves onto the next line of code
> - `continue`: skips any remaining code in the current iteration of the loop, and immediately starts the next iteration from the beginning of the loop

> [!example]- extra info
> Basically all graphical applications including games run on something known as a _main loop_, this is due to the fact they need to run at _`n` frames per second_, so simply looping is a logical solution to that.
> This is an example scaffolding of a _main loop_:
>
> ```cpp
> bool running = true;
>
> while (running) {
> 	process_input();
> 	update_state();
> 	render_frame();
> }
>
> cleanup();
> ```

### too many if's - switches

`switch` statements are a somewhat simplistic addition, they simply replace `if` statements if you want to check a variable that can have many possible values, they are often used together with [[types#^enums|enums]]:

```cpp
enum FooBar {
    FOO,
    BAR,
    BAZ
};

int main() {
     FooBar current = BAR;

    switch (current) {
        case FOO:
            printf("foo\n");
            break;
        case BAR:
            printf("bar\n");
            break;
        case BAZ:
            printf("baz\n");
            break;
        default:
            printf("Invalid value\n");
            break;
    }

    return 0;
}
```

Before you say this is pointless and you could just stack `if`'s - _yes you could_ but:

```c
if (current == FOO) {
    printf("foo\n");
} else if (current == BAR) {
    printf("bar\n");
} else if (current == BAZ) {
    printf("baz\n");
} else {
    printf("Invalid value\n");
}
```

Is this really more _readable_ for you ?

There is also the original reason why `switch` statements were introduced in the first place, which is that a switch statement can be optimized into a so called _jump table_

This means that in the compiler program a `switch` wouldn't have to actually perform the check logic that the `if` would and instead the compiler would precompute the comparisons allowing for immediately jumping to the correct _branch_

Unfortunately in recent years this argument lost a lot of it's merit since compilers have gotten smart enough to detect when a stack of `if`'s is used in place of a `switch` and they often get optimized the same way

### the simplest one - return

`return` is probably the simplest control flow statement of them all

> [!important]
> It can only be used inside a function [[functions#localized sin - scopes|scope]], and when used there immediately exits that function going back to where the function was called
> If the function has a return [[types|type]] then the `return` will expect an instance of that [[types|type]] to return as the return value of that function

Generally you almost always want to return from a function at it's end:

```cpp
int add(int a, int b) {
	return a + b;
}

int main() {
	printf("add: %d", add(69, 420));
}
```

But there is also an often overlooked technique called _early return_, this should be used if the operation your function is performing has a state that immediately completes the operation, for example:

```cpp
float divide(float a, float b) {
	if (b == 0.0) {
		return 0.0;  // can not divide by 0
	}
	
	if (a == 0.0) {
		return 0.0;  // 0 divided by anything is 0
	}
	
	return a / b;
}
```

The _early return_ here covers the 2 cases where we don't actually need to perform the division since we instantly know the result

This is a very helpful and underutilized technique (at least by beginner devs), so I would recommend you get familiar with it, you will thank me later

### shadow wizard money gang - goto

> [!warning]
>
> ### Feel free to skip this section for now!
>
> This section will be a bit more complicated and information dense, this is because you really shouldn't be using `goto`'s as an absolute beginner and at the point where you are ready for them this should be quite understandable

`goto`'s have a bad reputation these days and you won't find them in most new languages, but when used correctly they can be very beneficial

> [!important]
> A `goto` allows you to create a _named_ point in a [[functions#localized sin - scopes|scope]] and jump the program execution to it, there are many caveats to using this and it can cause serious issues though

This is an example adapted from the [Linux kernel codebase](https://github.com/torvalds/linux) (remember this GitHub repo is not the development platform for Linux, this is simply a mirror of the code):

```cpp
int init_device(void) {
    int status = 0;
    void *buffer = NULL;
    void *hardware_handle = NULL;

    buffer = malloc(1024);
    if (!buffer) {
        status = -1;
        goto out;          // nothing to clean up
    }

    hardware_handle = acquire_hardware();
    if (!hardware_handle) {
        status = -2;
        goto out_buffer;   // need to free buffer
    }

    // main logic (omitted here)
    printf("Device initialized successfully\n");

    // success path falls through to cleanup
    release_hardware(hardware_handle);

out_buffer:
    free(buffer);

out:
    return status;
}
```

You may realize this is more or less just _early returns_ from the last chapter, and you would be right, but the difference is that here we need to clean up certain things before returning from this function, but depending on the place where we return there are different things to clean up

In a situation like this you can do 3 things:

- write convoluted `if` statements controlling the cleanup - this is impractical
- repeat the cleanup code at each return manually - this bloats the code, makes it less readable and makes it so that if the cleanup changes you have to edit the cleanup code in multiple places instead of 1
- use `goto`'s like in the example, which make this simple and quite elegant in my personal opinion

#### the modern counterpart - defer

Due to the issues described above most new languages implement `defer` instead of `goto`

> [!important]
> `defer` simply queues actions inside a [[functions#localized sin - scopes|scope]] and executes all of them one by one when that [[functions#localized sin - scopes|scope]] ends

You can probably see how this replaces `goto` for the cleanup job it's performing in the example above

And since that is basically the only widely acceptable use of `goto`, `defer` replaces it fully in most cases

```go
func initDevice() error {
	var buffer []byte
	var handle *Hardware

	buffer = make([]byte, 1024)
	if buffer == nil {
		return fmt.Errorf("allocation failed")
	}
	defer freeBuffer(buffer)                        // runs when function exits

	handle = acquireHardware()
	if handle == nil {
		return fmt.Errorf("hardware unavailable")  // executes the 1 queued defer
	}
	defer releaseHardware(handle)                   // runs when function exits

	// main logic (omitted)
	fmt.Println("Device initialized")
	return nil                                      // executes the 2 queued defer(s)
}
```

This is a conceptual rewrite of the example above, and as you can see `defer` makes the cleanup much simpler and allows us to essentially forget about managing it
