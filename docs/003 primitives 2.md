# Primitives pt 2

## (Tagged) Unions

```rust
// declare name of the union and its variants
typ Packet: union {
    (),                     // empty v. (variant)
    Quit,                   // v. with no data
    Quit2: (),              // above is same as this
    Move: {x Int, y Int},   // annonymous struct
    Write: String,          // string
    Read: Arr<String, 4>,   // array of 4 strings
    Color: (Int, Int, Int), // tuple of 3 ints
};

// declaration of variable
let u1 = Packet;      // empty
let u2 = Packet:Quit; // initialized with v. Quit
u2 = Packet:Write(String:New("hello")); // changed to Write v.
u2 = Packet:Color((255,0,0));           // changed to Color v.
```

## Raw Pointers and Raw Arrays

```rust
unsafe {
    let p1 = raw<Int>;       // uninitialized pointer to int
    let p2 = raw<Int>:New(); // initialized to default (null)
    let p3 = raw<Int>:New(null); // explicitly to null

    let p4 = raw:Alloc<Int>(Int:New(99));
    // request memory from system and put it into a pointer

    let p5 = raw<Int>;
    p5 = p4;
    // move the address from p4 to p5

    *p5 = 4;
    // dereference pointer, assign

    raw:Delete(p5);
    // delete previously allocated memory
    // otherwise it leaks!

    let s = 25;
    let p6 = addressof(s);
    // make p6 point to the address of s
    // deleting it will crash!

    let parr = raw:Alloc<Int>(128);
    // request enough memory for 128 ints
    // gotta keep track of the size manually

    raw:Delete(parr, 128);
    // deleting less would leak!
    // deleting more would very likely crash!

}; // unsafe
```
