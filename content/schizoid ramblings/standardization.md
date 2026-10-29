---
publish: "true"
created: 2026-06-20T13:33:45.530Z
modified: 2026-10-28T22:36:30.000Z
published: 2026-10-28T22:36:30.000Z
topic difficulty: any
---

If a codebase shows any signs of growing above something like ~1k loc^\[lines of code], serious standardization should be considered

This is commonly handwaved away as "premature optimization" but i would argue that is it not, standardizing at least the most commonly used parts of a codebase this early ensures that later development will be simpler

> [!danger]
> It is also important to realize that a codebase not created with optimization in mind from the start will in 99.99% of cases never be optimized. This is why i argue later in this article that premature optimization does not exist, since it's either optimization from the get go or unoptimized code

---

This is less prominent in procedural codebases, but anything dabbling with [[functional composition]] or [[objects|object oriented]] styles should follow this advice

While procedural code is less impacted by this it is hard to refactor when technical debt accumulates, making it really important to have the knowledge and wisdom to know what and where to standardize from the beginning

---

Ultimately "premature optimization" does not exist it is simply what you call an inexperienced programmer trying to architect the whole codebase before writing it

In my opinion [[functional composition]] patterns allow for the best standardization since they allow for modularity, if a system is standardized up front but not hardcoded it becomes modular with clear bounds and rules

For further discussion of standardization and good practices look in:

- [[objects]]
- [[polymorphism]]
- [[global state]]

### general opinions

the opinions presented in [[error handling]] unfortunately result in 1 of 2 different impacts on a language:

1. the language becomes extremely verbose
2. the language needs to enforce standardization

---

_option 1_ can be desired in some situations but it generally leads to designing rust over again

rust forces explicitness and strict rules but doesn't standardize or provide a featured standard library.

this makes it annoying to work with, not because the compiler nags you constantly but because you need to work out your own standards and also work out the standards of other libraries, for example error enums and types, technically there is a somewhat "official way" but you can do it in many ways, which creates friction when using 3rd party libraries, which rust offloads most of it's basic functionality into

---

_option 2_ is in my opinion the correct choice, if the language provides a featured standard library, then that standard library enforces the standards in the language

for example go, error handling in go can also be done in many ways but the standard library creates a standard error expectation that is then fulfilled by 3rd party code
this makes the code predictable and simple even if verbose

this dynamic can be applied to many parts of a language, and the correct approach can be seen in the wild in languages like go or odin

---

c++ is a special case here since there really is no standard, you could point to c error handling and say that is the standard for c++ but with modern additions c++ can use many other standards just as well

this is where freedom in the language becomes both a curse and a blessing

since the language is so open ended anyone can use their preferred error handling method and be happy with it

on the other hand "anyone can use their preferred error handling method" which causes all libraries and 3rd party code to be different and in need of gluing together

I personally like the ability to do anything with the language that c++ provides but i can not in good faith argue that it is a good environment to learn or architect in

and i can not be sure if a well standardized language with freedom like c++ would in fact be a good language since that does not really exist currently

I unfortunately also have to agree with the creator of odin that people often abuse the freedom c++ gives by for example defining insane custom operators and such

while I think the user should have the ability to do that, it is unavoidable that some less experienced or just simply dumber^\[Don't take this too personally] people will abuse it in bogus ways
