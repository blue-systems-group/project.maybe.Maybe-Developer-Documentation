# Maybe Syntax

Generally, there're two kinds of maybe syntax: maybe block and maybe variable.

## Maybe Block
```java
maybe ("algorithm") {
    // do path 0
} or {
    // do path 1
} or {
    // do path 2
}
```

It defers choice for different code paths to runtime.

## Maybe Variable
```java
    int i = maybe("a") {1, 2, 3};
```

The variable `i` is maybe variable.

### Why not `int i = maybe("a") 1, 2, 3;`

If you have nested maybe variable:
```Java
    int i = maybe("a") 1, maybe("b") 2, 3, 4;
```

I don't know it should be:
```Java
    int i = maybe("a") {1, maybe("b") {2, 3, 4}};
```
or
```Java
    int i = maybe("a") {1, maybe("b") {2, 3}, 4};
```
or
```Java
    int i = maybe("a") {1, maybe("b") {2} 3, 4};
```

The complier doesn't know that as well, so it panics.

## Maybe Label
The string in `maybe ("label")` is maybe label.

The maybe label **can not contains "." or "$"**! Because we use mongodb to store data. And mongodb doesn't allow "." or "$" as key.
