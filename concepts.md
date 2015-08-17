# TODO Maybe statement

## Maybe Variable

```Java
int i = maybe("a") {1, 2, 3};
```

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

## TODO Maybe Block
# TODO labels
