---
publish: "true"
created: 2026-06-20T16:51:20.410Z
modified: 2026-10-28T22:47:58.000Z
published: 2026-10-28T22:47:58.000Z
topic difficulty: beginner
---

Global state is generally fine, if you know how to manage state in general

For example, do this:

```cpp
struct Ctx {
	foo bar;
	baz foobar;
	...
}

Ctx ctx;
```

Instead of:

```cpp
foo bar;
baz foobar;
...
```

==Global state should be as compact as possible==, this is to minimize accidental misuse of it

---

It is more code and setup but does not create global clutter, standardizing your global state this way early on allows you to get away with using global state for a surprising amount of time. More on [[standardization]].
In fact even some games use this kind of simple global state since it's really not that big of an issue

When can state like this become an issue ?

- when any threading is happening
- when it's poorly managed, e.g: used as storage for local volatile data

I would argue that most simple programs would benefit from doing state in a global way like this instead of worrying about dependency injection or any other method of organizing this

> [!important]
> This is where rust fails less experienced programmers and forces an unreasonable workflow, since globals like this are basically banned in rust
