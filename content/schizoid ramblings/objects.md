---
publish: "true"
created: 2026-06-20T14:55:46.110Z
modified: 2026-10-28T22:36:08.000Z
published: 2026-10-28T22:36:08.000Z
topic difficulty: moderate
---

### the good

Objects facilitate the most common [[standardization]] paradigm which is expecting a specific method name on an object

```cpp
struct Foo {
	void draw(const vec2& pos) {...}
}

template<typename T>
void draw_object(const T& obj) {
	obj.draw(pos);
}

int main() {
	Foo bar;
	
	draw_object(bar);

	return 0;
}
```

^monomorphic-example

But notice that this requires:

1. some kind of [[polymorphism]] (notice that the example uses templates instead of dynamic dispatch, more on that in the linked note)
2. that the api [[documentation|documents]] it requires a `draw(const vec2&)` method
3. and most importantly that the user reads this [[documentation]]

Otherwise this falls apart, to do anything in a codebase like this you need to constantly go back and forth between your code and docs or source

---

It doesn't help that most codebases using this paradigm are also "object oriented clean code" and the source is cluttered with hundreds of private/public, getter/setter definitions and such, making it hard to actually find what you want to know ^code-clutter

> [!important]
> It is important to note here that rust actually improves this and it is one of the things it should be praised for, interface/impl creates a clear definition of what is expected for an object to work in a specific context

Now this can be made somewhat acceptable with standardization, go does that with it's error types

Anything can be an error in go that implements an `Error() string` method, this is fine since it's fully standardized and it is expected in any scenario, but it is never explicitly signaled like it would be in rust with an impl

---

### the bad

Now to touch on bad practices, mainly dynamic dispatch

Consider this example:

```cpp
struct Drawable { 
	virtual void draw(const vec2& pos) const = 0; 
};

struct Foo : public Drawable { 
	void draw(const vec2& pos) const override {...} 
};

void draw_object(const Drawable& obj) { 
	obj.draw(pos);
}

int main() {
	Foo bar;
	
	draw_object(bar);

	return 0;
}
```

This is the same thing as [[#^monomorphic-example]], but as you can see it uses dynamic dispatch and inheritance instead of simple compile time type resolution

Now the first thing you might notice is how much more code we have to write to achieve the same effect, and most of the extra code does not add anything to our example here, of course it does mean something to the compiler but not to us reading the code

Then there is the performance impact which is also discussed here [[polymorphism#the other one]], the issue is that instead of resolving the call at compile time and hardcoding it, the compiler instead makes the call through vtables that are generated and traversed at runtime, which adds substantial overhead to something as simple as a function call
