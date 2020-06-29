# Choice.
### if-else
```c#
if (i == 0) {
    slib:log:OutL("i is equal to 0");
} else if (i == 1) {
    slib:log:OutL("i is equal to 1");
} else {
    slib:log:OutL("i is neither 0 nor 1");
};
```
### ?!
```c#
let i = let opt = OptionallyInt()
                ? ret opt.V()
                ! ret 0;
// if function succeeds:
// return result from scope, else return 0 from scope
// i = result of function,   else i = 0

let j = OptionallyInt() ? { ret $ } ! { ret 42 };
// (explicit scope blocks) if function succeeds:
// j = result of function, else j = 42

let k = OptionallyInt() ?! Terminate();
// if function succeeds:
// k = result of function, or else terminate program
```

### switch-case
```cpp
switch (w) {
    case 1: { // if w == 1
        slib:log:OutL("w is equal to 1");
    };
    case 2: { // if w == 2
        slib:log:OutL("w is equal to 2");
    };
    default: { // else, in any other case
        slib:log:OutL("w is neither 1 nor 2");
    };
};
```

### three-way comparison switch-case
```cpp
switch (a <=> b) {
    <: {
        slib:log:OutL("a is smaller than b");
    };
    =: {
        slib:log:OutL("a is equal to b");
    };
    >: {
        slib:log:OutL("a is bigger than b");
    };
};
```

### Observations:
- `;` at ends of `if`, `switch`, `case`: Signifies end of scope that doesn't return any object. Should be added automatically by the IDE if missed (by accident or intentionally), or errored out when ambigious.
- `else`, `default`: Ifs and switches need to be exhaustive.
- `()` and `{}`: Brackets are always necessary. So, for example, no short ifs like `if(true) do_thing();` or `if true {do_thing();};`.
- no `break` in `switch`: No fallthrough, so also no `break` necessary.

# Matching.
### simple match
```rust
match (x) {
    0: { slib:log:Out("0"); };
    1: { slib:log:Out("1"); };
    _: { slib:log:Out("don't care"); };
};
```

### Observations:
-

# Loops.
### manual-for
```c#
for (let i = 0; i < 5; i++) {
    slib:log:Out("{}", i);
    // prints "01234"
};
```

### for-in-range
```c#
for (let i in 0..4) {
    slib:log:Out("{}", i);
    // prints "01234"
};
```

### for-in-container
```c#
// container contains Ints from 0 to 5
for (let item in container) {
    slib:log:Out("{}", item);
    // prints "01234"
};
```

### while-do
```c#

```

### do-while
```c#

```

### break-continue
```c#
for (let i in 0..10) {
    if (i == 3) { continue; };
    if (i == 6) { break; };
    slib:log:Out("{}", i);
    // prints "01245"
};
```

### Observations:
-

