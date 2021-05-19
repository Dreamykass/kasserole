# Advanced concepts

## Depending on other concepts

```rs
con NonZero<T> {
    fun non_zero(self: T) -> T;
        // implementator is supposed to return a non-zero T
        // or panic/throw/terminate if not possible
}

imp NonZero<T> for <I32> {
    fun non_zero(self) -> Self {
        if self == 0 {
            terminate("NonZero<I32>:non_zero(): self is zero!");
        } else {
            ret self;
        }
    }
}



imp SafeDiv<G> for <G>
pre <                   // preconditions for this concept:
    G: NonZero<G>;      // G needs to satisfy NonZero<G>,
    G: Div<G, G, G>;    // and G also needs to satisfy Div<G, G, G>
                        // (which also specifies the / operator for G)
> {
    fun safe_div(a: G, b: G) -> G {
        a / b.non_zero()
    }       // default implementation, that uses only functions
}           // from the NonZero and Div concepts



// since I32 already satisfies Div (it could be from the std lib),
// and now also satisfies NonZero,
// it satisfies SafeDiv, despite there not being present
// an explicit implementation of SafeDiv for I32

#print("{}", SafeDiv:safe_div( 10,  2));    // prints "5"
#print("{}", SafeDiv:safe_div( 20, 10));    // prints "2"
#print("{}", SafeDiv:safe_div(100,  5));    // prints "20"
#print("{}", SafeDiv:safe_div(  2,  2));    // prints "1"

#print("{}", SafeDiv:safe_div(7, 0));       // terminates!
        // with message: "NonZero<I32>:non_zero(): self is zero!"
```


## Blanket implementation

```rs
con Description<T> {
    fun description(self: &T) -> String;
};

imp Description<T> for <ToString<T>> {
            // implementation of Description<T> for every type
            // that satisfies the concept ToString<T>

    fun description(&self) -> String {
        self.to_string()
    }
}

#print("{}", 5.description());          // prints "5"
#print("{}", "hello".description());    // prints "hello"
#print("{}", 12.75563.description());   // prints "12.75563"
```


## Generic concepts

```rs
con PrintEach<Collection<T>> {
    fun print_each(self: &Collection<T>);
}

// Vec<T> is a standard, generic,
// array-based, dynamically-sized collection

imp PrintEach<Collection<T>> for <Vec<T>> 
pre <T: ToString<T>> {          // precondition for this implementation:
    fun print_each(&self) {     // T must satisfy ToString<T>
        for element in self {
            #print("{}, ", element.to_string());
        }
    }
}


let integers = Vec:from_array([2, 5, 7, 12]);
            // type of integers is Vec<I32>
            // and I32 satisfies ToString
integers.print_each();
            // prints "2, 5, 7, 12"
```