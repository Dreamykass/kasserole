# Types and structs

## Type declarations

```rust
typ TypeName: ...;

// typ      - keyword that signifies that a new type declaration begins
// TypeName - name of the new type
// ...      - the type definition that will be bound to the TypeName
//            (can be a struct, a class, another type, an enum, etc)
```



## Type aliases

```rust
fun display(x: I32) { #print("{}", x); }

typ MyInteger: I32; // alias declaration, for a primitive


let x: MyInteger = 23;  // type of `x` is `MyInteger`
display(x);             // prints "23"
// a type alias can be implicitly treated as the aliased type
```

```rust
typ Color: (U8, U8, U8, U8); // alias declaration, for a tuple

let c = (123, 56, 34, 128); // type of `c` is `(U8, U8, U8, U8)`

let d = c as Color; // type of `d` is `Color`
// "conversion" from aliased type to the type alias, or the other way around,
// is "free"/no-op
```



## Structs

```rust
typ ColorNamed: struc { // struct declaration with named fields
    red: U8,            // (a regular struct)
    green: U8,
    blue: U8,
    alpha: U8,
};

let a = ColorNamed { // construction
    red = 64, green = 76, blue = 43, alpha = 128,
};

#print("{}", a.red); // access, prints "64"
```


## Unnamed fields

```rust
typ ColorTuple: struc ( // struct declaration with unnamed fields
    U8,                 // (a tuple-struct)
    U8,
    U8,
    U8,
);

let a = ColorTuple ( // construction
    64, 76, 43, 128,
);

#print("{}", a.1); // access, prints "76"

let b = ColorTuple ( // more explicit way of construction
    self.0 = 64, self.1 = 76, 
    self.2 = 43, self.3 = 128,
);
```


## Anonymous types

```rust
let pos = struc { // type of `pos` is an anonymous struct
    x: I32 = 35,
    y      = 62, // types of fields can be inferred
};

#print("{}", pos.x); // access of member, prints "36"


// anonymous types can also be declared in place of 
// return or parameter types in functions
fun fancy_addition(params: struc { a: I32, b: I32 }) 
-> struc { r: I32 } {
    struc { r = (params.a + params.b), }
}

let result = fancy_multiply( struc { a = 10, b = 4 } );

#print("{}", result.r); // prints "14"
```
