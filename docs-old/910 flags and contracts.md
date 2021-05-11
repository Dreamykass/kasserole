# Flags and contracts.
### Compiletime contracts.
```go
fun Divide(Int64 a, Int64 b)->Int64 {
    [ expect: b != 0 ]

    ret a / b
};

fun Main()->Int64 {
    let a = Int64<-console:GetInt();
    let b = Int64<-console:GetInt();

    Divide(a, b);

    ret 0
};
```
Compile-time error here at `Divide(a,b);`, as the second argument could potentially be equal to zero.

### Runtime contracts.
```go

```


### Flags.
```go
type MyInteger struct {
    flags [[
        zero
    ]];

public:
    Int64 m_int;

    func MyInteger(_in Int64)->MyInteger {
        m_int = _in;

        if (m_int == 0) {
            [[ zero = T ]];
        } else {
            [[ zero = F ]];
        };

        return;
    };
};
```

### Guarantees.
```c#
func Divide(a MyInteger,
            b MyInteger)->MyInteger
[[ F: b:zero ]] {

    ret a / b
};
```

### Observations.

### Hmm.
I've been thinking about another (potentially nice?) idea for that fictional language: "flags" (can't think of a better name right now).

Like let's say there's Opt<int>, which is like std::optional<int> in C++. Opt can have one flag: has_value.

To get the value from Opt, the flag needs to be true, otherwise it doesn't compile. How to guarantee the compiler that the flag is set, though?

It can be with an if that checks if the Opt has a value: if it does, then the flag has_value is guaranteed to be true.

And there could naturally be a function that takes Opt, but only with the has_value flag being true - so the caller needs to ensure that the flag is set with an if.

This could be nested and the like, and work with containers as well - can't iterate the container of Opts and take the value of each, unless you can prove the flag is set for every Opt.

...this would probably be a hell to implement, but oh my, it'd bring a lot of safety and make writing stuff a ton easier, I think