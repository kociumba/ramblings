---
publish: "true"
created: 2026-06-25T12:33:59.560Z
modified: 2026-10-28T22:40:56.000Z
published: 2026-10-28T22:40:56.000Z
topic difficulty: beginner
---

Since code files are essentially just text files, you’ll naturally want to write notes or text in them that won't actually be treated as code

You may want to _document_ something, write down your thoughts or simply let out some frustration when nothing seems to work (trust me it's normal)

> [!important]
> _Code comments_ are pieces of text in [[your first program#I didn't know this was a writing class - source files|source files]] which are not code

### single line comments

Most languages you can interact with will allow for writing code comments after a `//`, this allows the language to ignore all text up until the beginning of the next line

Some languages use `#` or `--`, quite honestly speaking only really `//` is somewhat standard and you will probably need to check your language specifically for what it uses

> [!important]
> These are _single line comments_ meaning they only ignore your text up until the beginning of the next line

Here is a table of some common languages and what they use:

| symbol | languages                                                              | example                |
| ------ | ---------------------------------------------------------------------- | ---------------------- |
| `//`   | C, C++, C#, Java, JavaScript, TypeScript, PHP, Swift, Go, Kotlin, Rust | `// this is a comment` |
| `#`    | Python, Ruby, PHP, Perl, Bash/Shell, R, PowerShell                     | `# this is a comment`  |
| `--`   | SQL, Lua, Haskell                                                      | `-- this is a comment` |
| `%`    | MATLAB, LaTeX                                                          | `% this is a comment`  |

This only covers a small selection, but as you can see `//` is the most ubiquitous and generally regarded as the standard _single line comment_ symbol

### multi line comments

If you have a lot to say or need to write long documentation sections, you will turn to _multi line comments_

These are supposed to allow for ignoring more text than just one line without repeating the comment symbol on each line

> [!important]
> _Multi line comments_ last from the _opening symbol_ up until the _closing symbol_, all text between them will be ignored and not treated as code

This is an incomplete list of _opening and closing symbols_ in different languages:

| _opening_/_closing_ | languages                                                                        |
| ------------------- | -------------------------------------------------------------------------------- |
| `/*`...`*/`         | C, C++, C#, Java, JavaScript, TypeScript, CSS, PHP, Swift, Go, Kotlin, Rust, SQL |
| `<#` ... `#>`       | PowerShell                                                                       |
| `=begin` ... `=end` | Ruby                                                                             |
| `%=` ... `=%`       | MATLAB                                                                           |
| `{-` ... `-}`       | Haskell                                                                          |

And an example with the most common `/*`...`*/`:

```cpp
/*
This function performs addition of two integers and returns the result

prams:
	- a: first integer in the addition
	- b: second integer in the addition
	  
returns:
	- the product of adding a and b
*/
int add(int a, int b) {
	return a + b;
}
```

Documenting a function like this of course quite comical but it showcases the concept of _multi line comments_ very well

> [!info]
> If you want to learn more about _code comments_ there is a lot more info in [[documentation]], this won't be as beginner friendly since it's not part of this _basics_ series, but there is a lot more info about the proper usage of _code comments_ and good practices
