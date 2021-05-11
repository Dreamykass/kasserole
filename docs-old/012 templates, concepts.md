
# Templated Functions

## Basic

### Wrong

```c#
tpl <typ T>
fun Add(a T, b T)->T {
    ret a + b // error here!
};

fun Main() { Add(1, 3); };
```

Error at `a + b`! Templates are concept-based - so when writing templated code, the programmer needs to specify exactly what attributes or qualities the types need to have - and that dictates what types can the templated code be instanced with.

### Correct

```c#
tpl <Addable T>
fun Add(a T, b T)->T {
    ret a + b // ok
};

fun Main() {
    Add(1, 3);     // ok
    Add(Foo, Bar); // possibly an error,
                   // if Foo and Bar don't fulfill concept Addable
};
```

Addable is a concept - a "requirement" - and any type that fulfills this concept can be instanced with this function.

In consequence, after the templated code is written, to find out what types should it be instanced with, only a single look at the declaration is needed. No surprises!

## Proper concepts

### Use

```c#
tpl <typ T, typ U>
fun ComplexFunction(arg1 T, arg2 U)
con <
    T: Movable, Copyable, Callable,
       EmptyCallable, Fooable, Somethingable;
    U: Addable, TemplateConceptable<T>;
> {
    ...
};
```

### Definition

```f#


```
