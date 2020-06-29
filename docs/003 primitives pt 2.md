# Primitives pt 2

## Unions

```rust
// declare name of the union and its variants
type Packet: union {
    (),         // empty v. (variant)
    Quit,       // v with no data
    Quit2: (),  // above is same as this
    Move: {x Int, y Int},   // v is an annonymous struct
    Write: String,          // v is a string
    Read: Arr<String, 4>,   // v is an array of 4 strings
    Color: (Int, Int, Int), // v is a tuple of 3 ints
};
```

## Raw Pointers and Raw Arrays
