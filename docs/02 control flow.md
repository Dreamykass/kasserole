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
let i = { let opt = OptionallyInt()
            ? ret opt.V()
            ! ret 0
        };

let j = OptionallyInt() ?! ret 0;
```

### switch-case
```cpp
switch (w) {
    case (1): {
        slib:log:OutL("w is equal to 1");
    };
    case (2): {
        slib:log:OutL("w is equal to 2");
    };
    default: {
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
    0: { slib:log:Out("zero"); };
    1: { slib:log:Out("one"); };
    _: { slib:log:Out("don't care"); };
};
```

### Observations:


# Loops.
### manual for
```c#
for (let i = 0; i < 5; i++) {
    slib:log:Out("{}", i);
    // prints "01234"
};
```

### for in range
```c#
for (let i in 0..4) {
    slib:log:Out("{}", i);
    // prints "01234"
};
```

### for each in container
```c#
// container contains Ints from 0 to 5
for (let item in container) {
    slib:log:Out("{}", item);
    // prints "01234"
};
```

### while do
```c#

```

### do while
```c#

```

### break and continue
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


# Exceptions.
### Try, catch, throw, finally.
```c#
try {
    throw Exception("");
} catch (slib:exc:LogicError e) {
    slib:log:Out("handling exception of type slib:exc:LogicError");
} catch (slib:exc:OutOfRange e) {
    slib:log:Out("can't handle exception of type slib:exc:OutOfRange, so rethrowing so it can be handled by the previous scope");
    throw;
} catch (Exception e) {
    slib:log:Out("handling exception of type Exception");
} catch (...) {
    slib:log:Out("handling exception of any type");
} finally {
    slib:log:Out("handled some exception, and doing things just before leaving the try scope");
};
```

### Panicking and recovering.
```
try {
    panic;
} recover {
    slib:log:Out("recovering from a panic");
};
```

### Observations:
- Catches ordered from most specific to least specific, as they're evaluated in order of declaration. All exceptions are supposed to inherit from Exception, so if `catch (Exception)` was first, the two `slib:exc:...` could not be caught.
- Panics don't have "payloads", and are supposed to be used only for stack unwinding, in situations where a part of a program has gotten into an unfixable situation. Therefore, they could be greatly optimized by implementation, hopefully, maybe.

# Other
### label/goto
```cpp
#LABEL LabelName;
...
goto LabelName;
```

