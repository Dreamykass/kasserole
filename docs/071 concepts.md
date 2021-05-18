# Concepts

## Basic concepts

```rust
con PlusOne<T> {           // concept declaration
    fun plus_one(self: T) -> T;    
}       // every implementation of this concept
        // must implement this function


imp PlusOne<T> for <I32> { // concept implementation
    fun plus_one(self) -> Self { // Self is type T, 
        self += 1                // so here it is I32,
    }                            // as specified in the concept
}

let a = 30;
let b = a.plus_one();
#print("{}", b);        // prints "31"
```


## Multiple types

```rust
// concept that describes addition
// abstracting over the left, right, and result types
con Add<A, B, R> {
    fun add(a: A, b: B) -> R;
}

// I32 + Bool should return an I32,
// which is a+1 if b is true, otherwise just a
imp Add<A, B, R> for <I32, Bool, I32> {
    fun add(a: A, b: B) -> R {  // types can be referred to
        a + (b as I32)          // by their concept names (A, B, R)
    }                           // or by their
}                               // imp names (I32, Bool, I32)

// Bool + I32 should return a Bool,
// which is false only if a is false and b is zero
imp Add<A, B, R> for <Bool, I32, Bool> {
    fun add(a: Bool, b: I32) -> Bool {
        a or (b as Bool) // true if either a or (b as Bool) are true
    } 
}


#format("{}", Add:add(10, true )); // prints "11"
#format("{}", Add:add(10, false)); // prints "10"

#format("{}", Add:add(true,  50)); // prints "true"
#format("{}", Add:add(false, 50)); // prints "true"
#format("{}", Add:add(true,   0)); // prints "true"
#format("{}", Add:add(false,  0)); // prints "false"

// let a: Bool = Add:add(35, 64);  // error!
        // can't find Add implementation for <I32, I32, Bool>
// Add:add(35, 64);                // error!
        // can't find Add implementation for <I32, I32, ?>
// Add:add(0.0, false);            // error!
        // can't find Add implementation for <F32, Bool, ?>
```

## Default implementation

```rs
con
```
