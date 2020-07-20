# Code Generation

## The problem

We have an array that we want to fill with strings. We know the strings at compile-time, and we can read them from a file. The file might be written manually, or it might be created by a build script, or retrieved from a server.

```rust
let fruits = [...];
```

## Trivial solution

Just have a function that reads strings from a file. Not really all that optimal though, at it's run-time, and so might hurt performance if there's lots of these strings.

```rust
let fruits = ReadFruitsFromFile();
```

## Code generation

The better (in some situations) alternative is code generation (codegen). It runs at compile-time. It's a scripting language, with different syntax from the actual code.

```py
let fruits = [
  @gen {
    file = open("stuff.txt")
    lines = file.readlines()

    for line in lines:
      line = line.trim()
      << "$line",\n
      # '<<' writes everything afterwards to code/source,
      #      up to a newline (in actual source, so not the \n character)
      # '$' calls or uses code, so '$line' becomes whatever the var 'line' has,
      #     '$foo()' becomes whatever 'foo()' returns, etc
  }
];
```

Where stuff.txt is:

```txt
pear
banana
mango
melon
grape
```

The actual code, after codegen runs, becomes:

```c#
let fruits = [
  "pear",
  "banana",
  "mango",
  "melon",
  "grape",
];
```

## A different solution

Compile-time expressions... Haven't wrote about them yet though.
