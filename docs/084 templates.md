
# Templates

## Basic templated functions

```rust
// fun display<T>(a: T) {
//     #print("{}", a);     // error!
// };                       // print requires T to be printable

fun display<T>(a: T)
pre T: Print {          // precondition:
    #print("{}", a);    // T needs to be printable
};

display(65);        // prints "65"
display("hello!");  // prints "hello"
display(3.14);      // prints "3.14"


// it can also be written as...
fun display(a: imp Print) {
    #print("{}", a);        // `imp Foo` type is shorthand
};                          // for a templated function
```


## Advanced templated functions

```rust
fun add<A, B, R>(a: A, b: B) -> R
pre <
    A, B, R: Print, Number;
        // all types need to be printable
        // all types need to be numbers
    exists: Add<A, B, R>;
        // there needs to exist an implementation
        // of the Add trait with these types
        // (that trait would also define the + operator)
> {
    let r = a + b;
    #print("{} + {} = {}", a, b, r);
    r
};


let _ = add(1, 5);          // prints "1 + 5 = 6"
let _ = add(67.2, 32.8);    // prints "67.2 + 32.8 = 100.0"
```
