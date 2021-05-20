# Classes and methods

## Classes vs structs

The difference is primarily the intention.
Structs are for "bag of data" kinds of types, 
while classes are for types with invariants (?).

- visibility: fields of structs are always public,
  while fields of classes are private by default 
  and must be explicitly made public

Other than the above, structs and classes 
are pretty much the same. They can both have methods,
constructors, etc.



## Classes

```rust
typ Color: class { // class declaration
    pub red: U8,
    pub green: U8,
    pub blue: U8,  // fields are public,
    pub alpha: U8, // accessible from anywhere
};

// access and construction is same as in case of structs...

let c = Color { // construction
    red = 64, green = 76, blue = 43, alpha = 128,
};

#print("{}", c.red); // access, prints "64"
```



## Methods and constructors

```rust
typ Counter: class {
    value: I32, // field is private
};              // (accessible only from this module)
                // (this includes the methods below)

imp Counter { // implementation block

    // Self - the type that the imp block is for,
    //        so in this case it is the Counter type
    // self - the concrete object that a method operates on,
    //        always of the Self type

    pub fun new(i: I32) -> Self { // equivalent to -> Counter
        Counter { value = i } // returns a new Counter
    }

    pub fun increment_by(&$self, x: I32) { // method mutates self
        self.value += 1;
    }

    pub fun get_value(&self) -> I32 { // method does not mutate self
        self.value
    }

    pub fun display(self) { // method consumes self
        #print("{}", self.value);
    }
    // these methods are public
}

let &counter = Counter:(10);

// Foo:new() is a special function name on a type,
// that can be called without specifying the name,
// so                    `Foo:new(param1, param2, param3)`
// is equivalent to just `Foo:   (param1, param2, param3)`

counter.increment_by(1);

let v = counter.get_value();
#print("{}", v); // prints "11"

Counter:increment_by(&$counter, 1); 
            // methods can be called as normal functions
            // where the first parameter is self

counter.display(); // prints "12"
```

