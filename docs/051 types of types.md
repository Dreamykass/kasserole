# Types of types

## Table of type types

|            | Nominal               | Structural      |
| ---------- | --------------------- | --------------- |
| Unit       | `struc T;`            | `Unit`          |
| Positional | `struc (A, B)`        | `(A, B)`        |
| Named      | `struc { a: A, b: B}` | `{ a: A, b: B}` |

## Nominal vs Structural

Nominal - can assign a to b, if they **contain** the same types.
```rs
let $a = (12, 65.34);   // mutable
let  b = (69, 35.3563);
a = b; // ok
```

Structural - can treat A like B, if they **are** the same types.
```rs
let $a = struc(12, 65.34);   // mutable
let  b = struc(69, 35.3563);
a = b; // error!
       // type of a is `anonymous_struct_1`
       // type of b is `anonymous_struct_2`
       // and so typeof(a) != typeof(b)
```

