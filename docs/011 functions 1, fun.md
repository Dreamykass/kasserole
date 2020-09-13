
# Functions

## Basic

```c#
fun Multiply(a Int, b Int)->Int {
    ret a * b
};

fun Main() {
    PrintLn("2 * 4 == {}", Multiply(1, 3));
};
```

## Overloading

### On arguments

```cpp
fun Add(a Int32, b Int32)->Int32 { ret a + b };
fun Add(a Flt32, b Flt32)->Flt32 { ret a + b };

Add(2, 4);        // calls the first overload
Add(7.3, 32.999); // calls the second overload
```

### On return type

```c#
fun Get()->Int32 { ret -1 };
fun Get()->Flt32 { ret 99.9999 };

let i Int32 = Get();    // calls the first function
let f Flt32 = Get();    // calls the second function
PrintLn("{}", Get()));  // error! ambigious overload
let a = Get();          // error! ambigious overload
```

If the overload is ambigious, the compiler is supposed to emit an error and halt.

### Explicit overload call

```c#
PrintLn("{}", Int32<-Get())); // prints "-1"
PrintLn("{}", Flt32<-Get())); // prints "99.9999"
```
