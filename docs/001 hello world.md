# Hello world

## Main

```cpp
import slib:log;

fun Main()->int {
    slib:PrintLn("Hello World!");
    ret 0
};
```

## Observations

- `import`: Keyword, imports the contents (exports) of the logging module (log) from the standard library module (slib). See "modules and slib".
- `fun`: Keyword, declares a function. See "basic constructs".
- `->int`: Return type of a function. See "basic constructs".
- `;`: Terminator, scope-ender. See "scopes".
- `slib:log:OutL()`: Call of a function from the `slib:log` space, that's in the `log` module in `slib` module. Function `OutL()` writes the argument(s) in a new line, to the console. See "modules and slib".
- `ret 0`: Keyword `ret` that returns an object from a scope/function. No semicolon, because the object leaves that scope/function. See "basic constructs".

## Style

### language

- keywords: `snake_case` (or `alllowercase` if short)
- preprocessor: `#SHOUTY_SNAKE_CASE`
- code generation: `@PascalCase`

### hmm

- types: `PascalCase` (or `alllowercase` if a short primitive)
- functions: `PascalCase`
- local objects: `snake_case`
- member objects: `m_snake_case`
- argument objects: `_snake_case`

## Punctuation

### language2

- `#` - preprocessor (prep)
- `@` - code generation (cgen)

### hmm2

- `;` - terminator, scope-ender
- `<>` - code generation arguments
- `()` - runtime call operator
- `,` - argument separator

### uhh

- `&` - reference?
- `*` - pointer, dereference
- `.` - direct access
- `->` - indirect access

### other

- `_` - discarder
