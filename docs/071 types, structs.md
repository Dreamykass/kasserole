# Structs

## Structs as just named tuples

```go
typ ColorTuple: Tup<UInt8, UInt8, UInt8, UInt8>;
// define type name 'ColorTuple' as tuple of types (...)
// not very convenient but still usable... though, is alpha first or last?

typ ColorStruc: struc {
    red UInt8;
    gre UInt8;
    blu UInt8;
    alp UInt8;
};
// define type name 'ColorStruc' as struct of types (...) with names (...)
// much better
```

## Structs with constructors and functions
