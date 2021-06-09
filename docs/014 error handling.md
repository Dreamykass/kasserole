# Exceptions and panics

## Exceptions vs panics vs results/options/etc

The "standard" way of error handling should be unions: 
`Result<T, E>`, `Option<T>`, `Either<A, B>`, or similar types.
- A function that opens a file could return a `Result<File, FileError>`,
  as it is a fallible operation, and failing is a real possibility,
  like in case the file with a given filename does not exist or is read-only.

Exceptions are for "high-level" errors, typically crossing the barrier 
between a library and the user.
- A method that saves some data on a structure representing a file-based database, 
  where the file is assumed to always be present and available for writing, 
  could throw an exception, as it is an unexpected state, 
  but at the same time a real possibility.

Panics are for "fatal" errors, where failure is unexpected,
and is violating some assumptions.
- Assertions about invariants could panic, as it is an unrecoverable error.


## Unions

```rs

```


## Exceptions

Exceptions are exclusively "checked" - a function that could raise exceptions,
needs to be explicitly marked as such. This includes the `main` function.

Exceptions can carry objects, and can be recovered from.

```rs
// function declaration
fun get_foo()
-> Foo              // return type of the function
!> FooUnavailable { // exceptions that the function could raise
    let foo = Foo:new();
    if foo.is_not_valid()
        raise(FooUnavailable:()); // raise an exception if not valid
    ret foo;                      // otherwise, return foo
};

try {                       // try block - if an exception is raised,
    let foo = get_foo();    // it will be caught in the cat block
    use_foo(foo);
} cat(x: FooUnavailable) {
    #print("Caught an exception!");
} fin {
    #print("Handled all exceptions now.");
};
```


## Panics

Panics are "unchecked" - a function that could panic,
does not need to be marked as such.

Panics do not carry any data, but can be recovered from, just like exceptions.
A program should recover from panics, only to log them or to notify the user - a 
program should not continue execution as normal after a panic.

```rs
fun get_bar()
-> Bar {
    let bar = Bar:new();
    if bar.is_not_valid()
        panic(); // panic if not valid
    ret bar;     // otherwise, return nar
}

try {
    let bar = Bar:new();
} rec {                  // rec block - for recovering from panics
    #print("Panicked!");
    abort();
};
```


