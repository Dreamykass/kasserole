# Primitives pt 1

## Scalar Types

- signed: `Int`, `Int8`, `Int16`, `Int32`, `Int64`, `Int128`, `ISizeT`
- signed: `UInt`, `UInt8`, `UInt16`, `UInt32`, `UInt64`, `UInt128`, `USizeT`
- floating point: `Flt32`, `Flt64`
- unicode: `Char`, `Char8`
- boolean: `Bool`
- byte: `Byte`
- unit/empty/null type: `()`

Both `Int` and `UInt` don't specify size - it's supposed to be chosen by the implementation.
`Char` is implementation-defined, while `Char8` is utf-8.

```rust
let a = Int;        // uninitialized
let b = 4;          // type of b is Int
let c = Int128(999);// initialized
```

## Compound Types

### Tuples

```rust
// declare tuples
let tuple = (12, "hello from the tuple");
let uninitialized_tuple = Tup<Int64, Str>;
let one_element_tuple = (9.9,);

// access elements of the tuple
uninitialized_tuple.0 = 77;
uninitialized_tupule.1 = "hello from the other tuple";

// move a tuple to another
let tuple2 = tuple;

// destructure a tuple
let (i, s) = tuple2;
i = 99;
s = "escape from new tuple";

// operate on every element of a tuple
let tuple3 = (1, 10.9, "foo");
comexpr for (auto e in tuple3) {
    slib:log:Out("{} ", e);
    // prints "1 10.9 foo "
};
// equivalent to:
//   slib:log:Out("{} ", tuple3.0);
//   slib:log:Out("{} ", tuple3.1);
//   slib:log:Out("{} ", tuple3.2);
```

### Arrays

```rust
// declare arrays
let array = [9,8,7,6];
let uninitialized_array = Arr<Int64, 4>;
let one_element_array = [9.9,];

// access elements of the array
uninitialized_array.0 = 44;
uninitialized_array.1 = 24;

// move an array to another
let array2 = array;

// for-in-container
for (let i in array2) {
    slib:log:Out("{}", v);
    // prints "9876"
};
```
