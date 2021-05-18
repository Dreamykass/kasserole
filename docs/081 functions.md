
# Functions

## Basic functions

```rust
// function declaration
fun multiplied(a: I32, b: I32) -> I32 {
    a * b
}


fun main() -> I32 {
    #print("{}", multiplied(2, 2)); // prints "4"
    #print("{}", multiplied(3, 6)); // prints "18"

    display(9); // prints "9"


    // functions can be declared inside other functions as well
    fun plus_5(z: &$I32) { // mutably borrows the object
        z += 5;
    }; // function declaration returns Unit
       // so ; is needed


    let $n = 34;
    plus_5(&$n); // mutably borrowed by the function
    display(n);  // prints "39"

    n // returned from function
      // same as `ret n;`
}


// functions can be declared in the code after they're called
fun display(x: I32) { // same as `-> Unit`
    #print("{}", x);
}
```


## Anonymous functions

```rust 
let a = fun _(arg: I32) -> I32 { arg + 10 } (2);
// the anonymous function is immediately called

#print("{}", a);  // prints "12"
```


## Call with named parameters

```rust
fun times_two(parameter: I32) -> I32 { parameter * 2 };

let r = times_two(parameter = 34);

#print("{}", r); // prints "68"
```
