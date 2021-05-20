# Advanced generics


## Generic over mutability

This is done with the `mut` keyword - for "mutability".

```rs
typ User: class {
    last_logged_in: Date,   // this field is private
};

imp User {
    pub fn new() -> User {  // public constructor
        User { last_logged_in = Date:now() }
    }

    pub fn last_logged_in_ref(&self) -> &Date {
        &last_logged_in     // public ref-getter (ref to immutable obj)
    }                       // for the last logged in date

    pub fn last_logged_in_ref_mut(&$self) -> &$Date {
        &$last_logged_in    // public ref-mut-getter (ref to mutable obj) 
    }                       // for the last logged in date


    // the above two methods can be abstracted away,
    // in one method that's generic over mutability:
    pub fn last_logged_in<m: mut>(&m self) -> &m Date {
        // m is a generic parameter representing mutability,
        // with two values: $ (mutable) and !$ (immutable)
        &m last_logged_in
    }
}


let user = User:(); // construction

let i1 = user.last_logged_in_ref();     // these two calls 
let i2 = user.last_logged_in<!$>();     // are equivalent
// both i1 and i2 are of type &Date (ref to immutable obj)

let m1 = user.last_logged_in_ref_mut(); // these two calls 
let m2 = user.last_logged_in<$>();      // also are equivalent
// both m1 and m2 are of type &$Date (ref to mutable obj)
```


## Generic over reference
