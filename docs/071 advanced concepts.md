# Advanced concepts

## Depending on other concepts

```rs
con NonZero<T> {
    fun non_zero(self: T) -> T;
        // implementator is supposed to return a non-zero T
        // or panic/throw/terminate if not possible
}

con SafeDiv<G>
pre G: NonZero<G> {                // precondition for this concept:
    fun safe_div(a: G, b: G) -> G; // G needs to satisfy NonZero<G>
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

imp SafeDiv<G> for <I32> {
    fun safe_div(a: I32, b: I32) -> I32  {
        a / b.non_zero()
    }
}


#print("{}", SafeDiv:safe_div( 10,  2));    // prints "5"
#print("{}", SafeDiv:safe_div( 20, 10));    // prints "2"
#print("{}", SafeDiv:safe_div(100,  5));    // prints "20"
#print("{}", SafeDiv:safe_div(  2,  2));    // prints "1"

#print("{}", SafeDiv:safe_div(7, 0));       // terminates!
        // with message: "NonZero:non_zero(): self is zero!"
```


## Blanket implementation

```rs
imp SafeDiv<G> for <G>
pre <                   // preconditions for this concept:
    G: NonZero<G>;      // G needs to satisfy NonZero<G>,
    G: Div<G, G, G>;    // and G also needs to satisfy Div<G, G, G>
                        // (which also specifies the / operator for G)
> {
    fun safe_div(a: G, b: G) -> G {
        a / b.non_zero()
    }       // in a blanket implementation,
}           // only functions can be used,
            // from concepts that this concept requires
            // (here it is NonZero and Div)


// now any type for which there are implementations of NonZero and Div,
// also satisfies SafeDiv
```


## Generic concepts?

```rs

```