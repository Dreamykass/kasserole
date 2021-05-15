# Overloading

## Basic

```rust
// fun half_invalid(a: I32) -> I32 {
//     a / 2
// }
// fun half(a: F32) -> F32 {
//     a / 2.0
// }
//              // error!
//              // can't have more than one function
//              // with the same name

fun half_i(a: I32) -> I32 {
    a / 2
}
fun half_f(a: F32) -> F32 {
    a / 2.0
}

// overload declaration
ove half: { // overload needs to have an unique name
    half_i,
    half_f,
}

// overload use
fun main() {
    #print("{}", half(10));     // calls half_i, prints "5"
    #print("{}", half(888.8));  // calls half_f, prints "444.4"
}
```

## Overload variants

```rust
fun zero_b() -> Bool { false }
fun zero_i() -> I32 { 0 }
fun zero_f() -> F32 { 0.0 }

ove zero: {
    zero_b,
    zero_i,
    zero_f,
}

fun main() {
    // #print("{}", zero());    // error!
                                // ambigious overload call

    // let a = zero();          // error!
                                // also an ambigious overload call

    let b: Bool = zero();       // implicitly chosen variant, calls zero_b
    let c = zero<I32>();        // explicitly chosen variant, calls zero_i

    #print("{}", zero<F32>());  // calls zero_f, prints "0.0"
}
```

## Concise declaration

```rs
ove one: {
    fun one_i() -> I32 { 1 }
    fun _() -> F32 { 1.0 } // anonymous function
}

fun main() {
    let a: I32 = one(); // calls one:one_i
    let b: F32 = one(); // calls one:anonymous_function_1

    #print("{}", a);   // prints "0"
    #print("{}", b);   // prints "0.0"
}
```
