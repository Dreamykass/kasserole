
# Functions with "autos"

## Basic

```c#
fun Substract(a aut, b aut)->aut {
    ret a - b
};

// the above might "transform" into the following

tpl <typ T1, typ T2, typ T3>
fun Substract(a T1, b T2)->T3
con <
    T1: OperatorSubstr<T2>;
    T3: ResultOf<OperatorSubstr<T1, T2>>;
> {
    ret a - b
};
```

```c#
fun Main() {
    Substract(4, 2);           // ok
    Substract(12.2, 99.2);     // ok
    Substract(true, (1, "a")); // error!
      // types "bool" and "Tup<Int64, String>"
      // don't implement concepts... etc
};
```

The idea: Very nice for small and quick functions and the like. The more complex the templated code, the better it is to explicitly define the required concepts.

Additionally, after the auto-code is written, as the user, it's very easy to see what concepts the compiler/IDE has generated for the code.
