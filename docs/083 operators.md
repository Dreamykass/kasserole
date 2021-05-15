# Operators

## Basic

```rust
fun add(a: I32, b: I32) -> I32 {
    a + b
}
fun add_5(x: I32) -> I32 {
    x + 5
}

// infix operator function declaration
ope add: { infix add, }  // operator name can be shared
                        // with the target function or other operators

// prefix and postfix operator function declaration
ope add_5_prefix:  { prefix add_5,  }
ope add_5_postfix: { postfix add_5, }


// operator use
fun main() {
    let a = 12 add 20; // evaluates to `= add(12, 20);`

    #print("{}", a);   // prints "32"

    let c = add_5_prefix 10;  // evaluates to `= add_5(10);`
    let d = 55 add_5_postfix; // evaluates to `= add_5(55);`

    #print("{}", c);   // prints "15"
    #print("{}", d);   // prints "60"
}
```

## Combined with overloading

```rust
fun sum_2(a: I32, b: I32) 
    -> I32 { a + b }
fun sum_3(a: I32, b: I32, c: I32) 
    -> I32 { a + b + c }
fun sum_4(a: I32, b: I32, c: I32, d: I32) 
    -> I32 { a + b + c + d }
fun sum_5(a: I32, b: I32, c: I32, d: I32, e: I32) 
    -> I32 { a + b + c + d + e }

// overload declaration for the above functions
ove sum: {
    sum_2, sum_3, sum_4, sum_5,
}

// operator declaration for the overload
ope sum: {
    prefix sum,
}

// advanced operator use
fun main() {
    let a = sum 1 1 1;
    // the above evalates to `= sum(1, 1, 1);`
    // which further evaluates to `= sum_3(1, 1, 1);`

    let b = sum 1 2 3 sum 10 40;
    // same as `= sum(1, 2, 3, sum(10, 40));`
    // and `= sum_4(1, 2, 3, sum_2(10, 40));`

    #print("{}", a);   // prints "3"
    #print("{}", b);   // prints "60"
}
```

## Concise declaration

```rust
// more concise operator declaration
ope div: {
    postfix fun _(a: I32, b: I32) -> I32 { a / b },
    // the above is an anonymous function
}

fun main() {
    let a = 10 5 postfix;
    #print("{}", a);   // prints "2"
}
```

## Custom symbols

```rust
fun display(x: I32) { #print("{}", x); }

ope 'd': { prefix display, }
// above is same as `ope d: ...`

// non-ascii-alphanumeric names need to be inside single quotes
ope 'Δ': { prefix display, } 
ope '📺': { prefix display, }

fun main() {
    d 5;    // prints "5"
    Δ 12;   // prints "12"
    📺 63;  // prints "63"
}
```
