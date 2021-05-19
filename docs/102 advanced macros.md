# Advanced macros


## Variadic macros

```rs
// macro declaration:
// this macro takes one identifier and many expressions
// and returns many statements
mac append_many_to_vec(#i: Ident, #es: Many<Expr>) -> Many<Statm> {
    #for #e in #es {
        #i.push(#e);
    }
}

let vec = Vec:from_array([0, 1, 2]);


// macro instantiation:
#append_many_to_vec(vec, 6, 7, 8, 8+1);

// the above expands to:
vec.push(6);
vec.push(7);
vec.push(8);
vec.push(8+1);

#debug_print(vec); // prints something like:
                   // "[0, 1, 2, 6, 7, 8, 9]"
```

