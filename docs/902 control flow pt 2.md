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

