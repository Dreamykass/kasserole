# Arrays and Tuples

## Tuples

```rust
// tuple variables
let tuple = (12, "hello from the tuple");
let explicit_tuple = Tup:(16, "hey");
let more_explicit_tuple = Tup<i32, Str>:(16, "hey");
let uninitialized_tuple: (I64, Str);
let one_element_tuple = (9.9,);

// access elements of the tuple
#print("{}", tuple.0);  // prints "12"
#print("{}", tuple.1);  // prints "hello from the tuple"

// destructure a tuple
let (i, s) = tuple;
#print("{}", i);    // prints "12"
#print("{}", s);    // prints "hello from the tuple"
```

## Arrays

```rust
// array variables
let array = [6,7,8,9];
let explicit_array = Arr:(1,2,3,4);
let more_explicit_array = Arr<I64, _>:(1,2,3,4);
let super_explicit_array = Arr<I64, 4>:(5,6,7,8,9);
let uninitialized_array: Arr<I64, 4>;
let one_element_array = [13,];

// access elements of the array
#print("{}", array.0);    // prints "6"
#print("{}", array.1);    // prints "7"
#print("{}", array.[1]);    // access same as above, prints "7"
#print("{}", array.[2]);    // prints "8"
```
