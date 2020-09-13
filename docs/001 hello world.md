# Hello world

## Main

```cpp
import slib:fmt;

fun Main()->int {
    slib:PrintLn("Hello World!");
    ret 0
};
```

## Style

### language

- keywords: `snake_case` (or `alllowercase` if short)
- preprocessor: `#SHOUTY_SNAKE_CASE`
- code generation: `@PascalCase`

### names

- types: `PascalCase`
- functions: `PascalCase`
- local objects: `snake_case`
- member objects: `m_snake_case`
- argument objects: `_snake_case`
