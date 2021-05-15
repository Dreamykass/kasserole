# Unions and Pointers

## (Tagged) Unions

```rust
// declare the union and its variants
typ Packet: union {
    Quit,                     // variant that holds no data
    Quit2:  Unit,             // above is same as this
    Move:   {x: I32, y: I32}, // annonymous struct variant
    Write:  String,           // string variant
    Read:   Arr<String, 4>,   // array of 4 strings variant
    Color:  (I32, I32, I32),  // tuple of 3 integers variant
};

// declaration of a variable
let u1: Packet;       // uninitialized
let u2 = Packet:Quit; // initialized with the Quit variant

let u3 = Packet:Write:(String:("hello")); // init from the Write variant
let u4 = Packet:Color:((255,0,0));        // init from the Color variant
let u5 = Packet:Color:new((128,128,128)); // same as above
```

## Raw Pointers

```rust

```
