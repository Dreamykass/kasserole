# Operators and the like

## Access

### space `:`

```go

```

### direct `.` and indirect `->`

```cpp

```

### cascade `..` and `->>`

```cpp
GetComplexStruct();
   ..  direct_member_1 = "";
   ..  direct_member_2 = 55;
   ..  direct_method();
   ->> indirect_member = 3.14;
   ->> indirect_method();

// the above is equal to:
let foo = GetComplexStruct();
    foo.direct_member_1 = "";
    foo.direct_member_2 = 55;
    foo.direct_method();
    foo->indirect_member = 3.14;
    foo->indirect_method();
```

## Stand-ins

### placeholder `_`

```go

```

### foo `$`

```go

```

### pipeline `|>`

```f#
fun IfWeaklyEqual(a String, b String)->Bool {
    ret a |> ToUpper
};

let result = "hello";
    |> ToUpper();
    |> Trim();

// equivalent to:
let result = "hello";
    result.ToUpper();
    result.Trim();

???
```
