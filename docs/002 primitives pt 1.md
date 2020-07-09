# Primitives pt 1

## Scalar Types

- signed integers: `Int`, `Int8`, `Int16`, `Int32`, `Int64`, `Int128`, `ISize`
- unsigned integers: `UInt`, `UInt8`, `UInt16`, `UInt32`, `UInt64`, `UInt128`, `USize`
- floating point: `Flt32`, `Flt64`
- text: `Char`, `Ascii`
- boolean: `Bool`
- byte: `Byte`
- empty-type: `()`
- no-type: `void`
- no-value: `null`

Both `Int` and `UInt` don't specify size - it's supposed to be chosen by the implementation.

```rust
let a = Int;              // uninitialized
let b = 4;                // type of b is Int
let c = Int128:(999);     // initialized
let d = Int128:New(1001); // same as above
```

## Compound Types

### Tuples

```rust
// declare tuples
let tuple = (12, "hello from the tuple");
let explicit_tuple = Tup(45, "heyo");
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
```

### Arrays

```rust
// declare arrays
let array = [9,8,7,6];
let explicit_array = Arr<Int64>:New(1,2,3,4);
let uninitialized_array = Arr<Int64, 4>;
let one_element_array = [13,];

// access elements of the array
uninitialized_array.0 = 44;
uninitialized_array.1 = 24;

// move an array to another
let array2 = array;

// for-in-container
for (let i in array2) {
    slib:Print("{}, ", v);
    // prints "9876"
};
```
