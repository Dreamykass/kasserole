# Functions.
## Code.
```cpp
import slib:log;

fun Multiply(int a, int b)->int {
    ret a * b
};

fun Multiply(double a, double b)->double {
    ret a * b
};

fun Main()->int {
    slib:log:OutL("2 * 4 == {}", Multiply(1, 3));
    slib:log:OutL("4.5 * 45.9 == {}", Multiply(4.5, 45.9));
    ret 0
};
```

## Observations:
- `fun Multiply(int a, int b)->int`: Function with two arguments, `int a` and `int b`, that returns an `int` from the function scope.
- `slib:log:OutL("2 * 4 == {}", Multiply(1, 3));`: Writes to console, as before. First argument is a string, second is the argument that's inserted/parsed into the `{}`.
- Two `fun Multiply()` functions: Function overloading based on arguments. See down.
- Functions before `fun Main()`. Otherwise the calls in `fun Main()` wouldn't "link" to the actual functions, and an error would be emitted.

# Overloading.
## On Arguments.
```cpp
fun Add(int a, int b)->int { ret a + b };
fun Add(double a, double b)->double { ret a + b };

Add(2, 4);        // calls the first function
Add(7.3, 32.999); // calls the second function
```

## On return type.
```c#
fun Get()->int { ret 0 };
fun Get()->double { ret 99.9999 };

int i = Get();          // calls the first function
double d = Get();       // calls the second function
slib:log:OutL("{}", Get())); // error! ambigious overload
let a = Get();               // error! ambigious overload
```
If the overload is ambigious, the compiler is supposed to emit an error and halt.

## Explicit overload call.
```cpp
fun Get()->int { ret 0 };
fun Get()->double { ret 99.9999 };

slib:log:OutL("{}", int<-Get()));    // prints "0"
slib:log:OutL("{}", double<-Get())); // prints "99.9999"
```

# Function and type no's and do's.
## Basic function.
```cpp
fun Add(int a, int b)->int { ret a + b };
```

## Same function, but fully explicit.
```cpp
    @MMI @I
fun const Add(int ref const a, int ref const b)
    ->int const nocatch nothrow { ret a + b };
```
## Observations:
- `@MMI`: "Main-Module-Inherit". Inherits code generation (cgen) settings from the main module. See "prep and cgen".
- `@I`: "Inherit". Inherits code generation (cgen) settings from the higher-level scope. Overwrites `@MMI`. See "prep and cgen".
- `fun const`: Function doesn't mutate anything that'd be outside of its body.
- `int ref`: Argument is passed by reference. See "structs and classes".
- `int const`: Argument can't mutated in the body.
- `->int const`: Returned object can't be mutated.
- `nocatch`: Scope doesn't catch exceptions.
- `nothrow`: Scope doesn't throw exceptions.

## Other keywords and names:
- `type mut`: States that an argument or a returned object is mutable.
- `type val`: Argument is passed by value (by copy if a primitive, or by move if a sophisticate)
- `fun mut`: States that the scope mutates objects outside of its body.
- `mut(Name1, Name2, ...)`: States that a scope mutates only the specified names.
- `docatch`: States that the scope can catch exceptions.
- `dothrow`: States that the scope can throw exceptions.
- `dothrow(Type1, Type2, ...)`: States that the scope can throw only the specified exceptions.