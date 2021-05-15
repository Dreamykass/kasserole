# Mutability and references

## References and borrowing
```rust
let a = 23;         // a is an immutable object of type I32

let b = &a;         // b is an immutable reference
                    // to an immutable object
                    // (a is "borrowed" by b)

let c: &I32 = &a;   // same as above, but explicitly typed

let d = *c;         // dereferences c
                    // &I32 into just I32

#print("{}", a);    // prints "23"
#print("{}", *c);   // same as above

// a = 573;     // not allowed! can't mutate an immutable object
```

## Mutability
```rust
let $a = 65;    // a is a mutable object of type I32

a = 100;        // ok, as a is mutable
a += 1;
a = a * 2;

#print("{}", a);    // prints "202"
```

## References and mutability
```rust
let a = 12;

let b = &a;         // b is an immutable reference to an immutable object
// *b = 2356;       // not allowed! can't mutate an object
                    // through a reference to an immutable object

let c = &$a;        // immutable reference to a mutable object
                    // a is mutably borrowed by c

*c = 996;
#print("{}", *c);   // prints "996"
#print("{}", a);    // prints "996"
```

## Mutable references

``` rust
let a = 4;
let b = 835467;

let $c = &a;        // c is a mutable reference to an immutable object
#print("{}", *c);   // prints "4"

c = &b;             // the object that c references is changed,
                    // but the borrowed objects themseves are not touched
#print("{}", *c);   // prints "835467"
```


