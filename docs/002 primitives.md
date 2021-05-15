# Primitives

## Scalar Types

- signed integers: `I8`, `I16`, `I32`, `I64`, `I128`, `ISize`
- unsigned integers: `U8`, `U16`, `U32`, `U64`, `U128`, `USize`
- floating point: `F32`, `F64`, `F128`
- text: `Char`, `Ascii`
- boolean: `Bool`
- byte: `Byte`
- unit type: `Unit`
- no-type: `Void`

```rust
let a: I16;             // uninitialized
let b = 4;              // type of b is I32
let c = I128:(999);     // initialized
let d = I128:new(1001); // same as above
let e: I64 = 32;        // explicitly typed
```
