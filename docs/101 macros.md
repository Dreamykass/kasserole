# Macros

(like rust's declarative macros)

Macros primarily work by textual substitution.
Macros do not take concrete values, as they are evaluated 
before the code is actually compiled.

Parameter and return types of a macro are its "rules", and are there 
primarily for validation and catching errors early.

For example, if a macro takes an identifier, then on instantiation,
an identifier passed to the macro needs to actually be a valid identifier
(`abcd` is a valid identifier, but `1234` is not).


## Basic macros

```rs
// macro declaration:
// this macro takes two expressions,
// and returns an expression
mac vec_from_two(#a: Expr, #b: Expr) -> Expr {
            // #a and #b are not values like I32 of String!
            // they are expressions,
            // that the macro was instantiated with
    {
        let v = Vec:new();
        v.push(#a);
        v.push(#b);
        v // v returned from this scope block
    } // this scope block is an expression,
};    // as it does not end with a semicolon


// macro instantiation:
let vec = #vec_from_two(3, 7 + 60);

// the above expands to:
let vec = {
    let v = Vec:new();
    v.push(3);          // #a and #b are substituted
    v.push(7 + 60);     // with `3` and `7 + 60`
    v                   // (which are both expressions)
};

#debug_print(vec); // prints something like:
                   // "[3, 67]"
```


## Basic macros example 2

```rs
// macro declaration:
// this macro takes one type and two expressions,
// and returns an expression
mac vec_of_type_from_two(#ty: Type, #a: Expr, #b: Expr) -> Expr {
    {
        let v = Vec<#ty>:new();
        v.push( {#a}.into<#ty>() );
        v.push( {#b}.into<#ty>() );
        v
    } 
}


// macro instantiation:
let vec = #vec_of_type_from_two(String, 12, "hello");

// the above expands to:
let vec = {
    let v = Vec<String>:new();
    v.push( {12}.into<String>() );          
    v.push( {"hello"}.into<String>() );
    v
};

#debug_print(vec); // prints something like:
                   // "[12, 'hello']"
```

