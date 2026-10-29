---
publish: "true"
created: 2026-06-20T17:36:24.160Z
modified: 2026-10-28T22:36:24.000Z
published: 2026-10-28T22:36:24.000Z
topic difficulty: moderate
---

Polymorphism typically referred to as generics or templates in some languages should not be abused

As interesting it is to put together some kind of elaborate templating system in c++ it is almost always slower than simply writing the code manually

---

It also introduces many issues related to type deduction and if reading code without an lsp can lead to confusion on what is what

```cpp
do_something("string");
do_something(69);
```

If `do_something` is defined in another file, then without an lsp you wouldn't be able to quickly tell me if it's just an override or if it's a template

> [!NOTE]
> The sane solution here is to allow polymorphism but disallow ambiguous overriding, but it's a language level solution

---

Templates and similar forms of polymorphism also suffer from combinatorial explosions:

```cpp
template<typename T, typename E, typename X>
auto do_somethin(T arg1, E arg2, X arg3) -> std::invoke_result_t<X, T, E> {...}

do_something("string", 69, [](const char*, int) {...});
do_something("string", 69.420, [](const char*, double) {...});
```

Now this for example will quickly cause issues, since it will create a unique versions of `do_something` for each set of params it is called with, since this isn't real polymorphism it will need to create those new versions even for instantiations where only 1 param changes.

Technically speaking this c++ code will be faster than similar code in a language that supports full polymorphism but that difference is very negligible on modern hardware and more importantly real polymorphism will not have to duplicate so much code in the compiled binary

### the other one

Dynamic dispatch is another form of polymorphism, this is common in object oriented languages like java, c# or oo style c++

And unfortunately it is a big mistake, and should be used as sparingly as possible in fact most code can do without it with no issues

Dynamic dispatch and it's issues are covered in more detail with an example here [[objects#the bad]]

This issue is especially prevalent in c++ where the compilation result of using inheritance are vtables which have abysmal performance, any job a dynamic dispatch vtable does can be done just as well with a map, a lookup table or compile time templating without sacrificing performance

The good thing is that most programmers these days realize that things like inheritance which causes these issues are generally a bad idea, even people withing object oriented circles admit it and typically don't use it any more

I will not go into more detail about this, but i recommend this excellent video by Casey Muratori about why and how this happens: !["Clean" Code, Horrible Performance](https://youtu.be/tD5NrevFtbU?si=LKKNCTcWGkzS4xXC)
