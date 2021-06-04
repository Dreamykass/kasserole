# Conversions

## Implicit conversions between number literals

```rs
// conversions from number literals to other number types are allowed,
// as long as loss of data does not occur

let f: I32 = 4;     // valid
                    // value of f is something like 4.000000000000000

let g: I128 = 9;    // valid
                    // even though number literals are I32 by default

let h: I32 = 0.347; // not valid
                    // loss of data

let i: U8 = 357345; // also not valid
                    // loss of data
```


## Explicit conversions via the `Into` concept

```rs
// this concept should look something like this
con Into<A, B> {
    fun into(self: A) -> B;
}

// example structure representing a 2D mathematical vector
typ Vector2f: struc { 
    x: F32,
    y: F32,
}

// implementation of a conversion from a tuple to the above structure
imp Into<A, B> for <(F32, F32), Vector2f> {
    fun into(self: (F32, F32)) -> Vector2f {
        Vector2f { x = self.0, y = self.1 }
    }
}

// usage
let v2f: Vector2f = (34.67, 12.01).into(); 
        // target type for the conversion is inferred
let integer = 0.5462467.into<I32>();
        // target type for the conversion is explicitly typed
```


## Implicit conversions via the `IntoImplicit` concept

```rs
// this concept should look something like this
con IntoImplicit<A, B> {
    fun into_implicit(self: A) -> B;
}

// implementation of an implicit conversion from a tuple to a Vector2f
imp IntoImplicit<A, B> for <(F32, F32), Vector2f> {
    fun into_implicit(self: (F32, F32)) -> Vector2f {
        Vector2f { x = self.0, y = self.1 }
    } // implementation is same as for the Into concept
}

// usage
let v2f: Vector2f = .(99.99, 111.11); // note the dot before the tuple
let integer = .0.23642013; // same as above
```

