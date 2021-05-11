
# Spaces

```c#
spa foo {
    fun XYZ()->... {...};
}

spa bar {
    fun XYZ()->... {...};

    spa nested {
        fun ABC()->... {...};
    }
}

fun Main() {
    foo:XYZ();
    bar:XYZ();
    bar:nested:ABC();
};
```

`name:name` <- the `:` is used to access names from (name)spaces
