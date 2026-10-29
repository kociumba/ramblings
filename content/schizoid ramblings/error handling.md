---
publish: "true"
created: 2026-06-20T11:10:01.900Z
modified: 2026-10-29T12:02:20.000Z
published: 2026-10-29T12:02:20.000Z
topic difficulty: beginner
"\n```odin\ndo_something ": proc() -> Maybe(int) {
---

Exceptions are retarded and break control flow, they also can have a considerable performance impact, ==NEVER USE EXCEPTIONS (when possible)==

I say this since exceptions are modeled after human patterns of though instead of how computers work, this causes issues when a program written with a language tailored for computers has to perform actions tailored for human thinking, mainly performance hits due to stack unwinding, and control flow redirection with `try/catch/finally` blocks

Specific performance impacts of exceptions ins different languages are hard to discuss since they vary between compilers and language versions due to backend implementations

But the biggest issue of exceptions is universal to all implementations, that is **they hijack control flow**, making the execution order of your code unpredictable

The core idea is nice: _"just write your code, and if anything happens the language will take care of it"_, but in languages where the user is supposed to have the control like c++, this can easily introduce lifetime bugs such as use after frees or null pointer derefs, to show an admittedly contrived example:

```c++
struct Resource {
    void action(bool t) { if (t) { throw "error"; } }
};

void process() {
	Resource* r1 = nullptr; 
	Resource* r2 = nullptr;
    try {
	    r1 = new Resource(); 
	    r1->action(false); 
	    delete r1;

        r2 = new Resource(); 
        r2->action(true);  // execution jumps to handler
	    delete r2;
    } 
    catch (...) {
	    delete r1;  // double free, since there is no way to know if r1 or r2 threw
	    delete r2;  // if r1 throws, this frees unallocated memory
    }
}
```

As manufactured as this example is this bug never happens with error returns since the control flow itself tells the error handler which resource it should use:

```c++
struct Resource {
    bool action(bool t) { return t; }
};

bool process() {
    Resource* r1 = new Resource();
    if (!r1->action(false)) { 
	    delete r1;
		return false;
	}
    delete r1;

    Resource* r2 = new Resource();
    if (!r2->action(true)) {
	    delete r2
        // no reason to ever reference r1 here
        return false; 
    }

    delete r2;
    return true;
}
```

This code is also more self [[documentation|documenting]] since reading it you can immediately see which error is being handled where, instead of having to mentally jump to the exception handler to see what happens on the error path

---

For C enum or int returns are the only verbose option, you can also go with a hidden "error backend" that the user has to retrieve from manually, but most of the time that will go unchecked

Best error handling is possible with monadic types and multiple return value support:

```odin
do_something :: proc() -> Maybe(int) {
	return 69;
}
```

> [!info]
> `Maybe(T)` in odin is actually simply a tagged union of type `T` and `nil`, in fact the thing that enables most of these nice paradigms are native tagged unions in the language, which are in my honest opinion in the top 10 of most useful features a programming language can implement

```go
func do_something() (int, error) {
	return 69, nil
}
```

---

The typical implementation of `Result` types is needlessly complex and does not account for any duality of state.
In rust or c++ the result either represents a failed state or a success, a partial success or failure is not possible to account for.

> [!info]
> Many people will argue that if you want partial success in a rust `Result` you should just return a struct or a tuple in the success branch, which then communicates the partial state. But this approach is fully [[standardization|unstandardized]], and as such belongs in the same pile of "do it yourself" issues that rust users often use to argue superiority over c++
> The model itself should take into account partial state and allow for it innately, and it wouldn't even be that hard in rust, you just have to use something else than `Result`

My opinion on the matter is that in situations with a binary outcome an odin style `Maybe` is sufficient and for situations where the state is more complex and may create a partial failure you want a `Result` type that can hold both values instead of one or the other, which is more efficiently solved by supporting multiple return values.

Also in many cases a simple `bool` return from a function is more than enough, this is the most self [[documentation|documenting]] paradigm next to a `Maybe` type, since there is no ambiguity on what it means or how to handle it, an excellent example of this kind of error handling is [ImGui](https://github.com/ocornut/imgui) (note that it's not really error handling in imgui, it's result handling, but the same mechanisms can be applied to )
