---
publish: "true"
created: 2026-06-24T12:08:21.690Z
modified: 2026-10-28T22:41:38.000Z
published: 2026-10-28T22:41:38.000Z
topic difficulty: beginner
---

As the famous saying says: "The only 2 hard things in programming are cache invalidation and naming things"

The basics of naming things are pretty simple, since in virtually all languages rules for it are going to be mostly the same

> [!important]
>
> - names can not have spaces in them
> - names can not use characters reserved by the language itself

This results in a few mostly universal naming styles:

- `snake_case`: uses lowercase, and replaces spaces with `_`
  - `kebab-case`: some languages allow using `-` like you would `_` in `snake_case` though this is rare
  - `SCREAMING_CASE`: impractical due to using all uppercase letters and `_` instead of spaces, but conventionally used in some places
- `PascalCase`: removes spaces entirely, instead capitalizing each new word
- `camelCase`: same as `PascalCase` just starts the name with a lowercase character

Now unlike some tutorials and guides I won't pretend here like you _have_ to use these in a some specific places

Generally it's more important to have a consistent pattern of usage with these instead of making sure you use them in a standard way

That being said there is one convention which is goo to follow regardless (at least in languages like c or c++)

Using `SCREAMING_CASE` for [[variables#constant variables ? - constants|constants]] and constant like defines (specific to c/c++), this is generally a good idea since it immediately conveys the information that this thing is a [[variables#constant variables ? - constants|constant]] to the reader and lowers the probability of naming conflicts between normal [[variables]], [[functions]] and [[types]]

```cpp
#define BUFFER_SIZE 1024

int main() {
	char buffer[BUFFER_SIZE];
	
	// do something with the buffer
	
	return 0;
}
```

Other than this my personal preferences are:

- use `snake_case` for all [[variables|variable]] and [[functions|function]] names
- use `PascalCase` or `snake_case` for [[types|type]] names

This is very simple compared to what the industry typically advocates for

If you were to go ask a university professor or take a java course you would probably be taught:

- use `PascalCase` for class/type names
- use `camelCase` for methods
- use `snake_case` for local variables and parameters

Which in my opinion simply clutters the code and makes it _less readable_

> [!example]- extra info
> Go is a special language that basically enforces the use of `PascalCase` and `camelCase` since symbols starting with an uppercase character are considered _public_ and symbols starting with a lowercase character are considered _private_

### spelling bee nightmare - name length

Now how to actually name your code using the cases we covered above ?

Well the rules are actually quite simple:

- the name should describe what the thing is and what it does
- don't overdo it like e.g. `D3D12CreateVersionedRootSignatureDeserializer` (example from D3D12 the Microsoft GPU api, read more [here](https://learn.microsoft.com/en-us/windows/win32/direct3d12/direct3d-12-reference)

As you can see it is really quite simple, but as with everything the hard part is striking the balance

I won't be covering in detail here how to strike that balance, since it depends on many factors:

- are you working alone or with a team
- are documenting your code
- which case you are using
- is the code simple to read or hard to read or hidden
- are you writing code for a library or application

And probably a few more which i can not think of right now, but what I can recommend it to read about and use some well written and established libraries like:

- [SDL3](https://github.com/libsdl-org/SDL)
- [ImGui](https://github.com/ocornut/imgui)
- [Raylib](https://github.com/raysan5/raylib)

Getting to know these will give you a good sense of how to name things and which names should and which shouldn't be verbose
