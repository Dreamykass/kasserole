# Templates

(like rust's procedural macros)

Templates, like macros, can take identifiers, types, expressions, tokens.
And like macros, they are evaluated before the code is actually compiled.

The major difference is, templates don't work 
by just textual substitution - they can execute arbitrary code,
before they expand to tokens the like.


## Basic function-like templates

```rs
// template declaration:
// this template takes an identifier,
// and returns tokens
tem make_function(name: Ident) -> Many<Token> {
    let f = #format(
        "fun {} () -> I32 \{ 42 \};",
        name.to_string()
    );
    f.parse().unwrap() // parse the string into tokens
};


// template instantiation:
#[make_function(foobar)];

// the above expands to:
fun foobar() -> I32 { 42 };


#[make_function(get_42)];
let x = get_42(); // the generated function 
                  // can be called like any other
```


## Basic function-like templates example 2

```rs
// template declaration:
// takes a string literal,
// and returns a string literal
tem palindrome(lit: Literal:Str) -> Literal:Str {
        // this template should take a string literal,
        // and if it's not a palindrome then compilation should halt,
        // otherwise it should expand to the string literal
    
    if lit != lit.reversed() {
        terminate("not a palindrome!");
    } else {
        ret lit;
    }
};


// template instantiation:
let p = #[palindrome("wow")];

// the above expands to:
let p = "wow";


// let r = #[palindrome("aaaaab")];
    // error! compilation halts with a message "not a palindrome!"
```

