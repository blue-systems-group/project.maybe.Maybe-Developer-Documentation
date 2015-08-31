# Maybe Syntax and Rewriter
We need rewrite all maybe syntax to ordinary Java codes.

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

to

```java
switch (maybeService.get("algorithm")) {
    case 0:
        // do path 0
        break;
    case 1:
        // do path 1
        break;
    case 2:
        // do path 2
        break;
    default:
        System.err.println("maybe label algorithm got choice out of range.");
        // do path 0
        break;
}
```

## Maybe Variable
```java
int batteryLevel = maybe("battery") {10, 15, 20, 30};
```

to

```java
int batteryLevel = 10;
switch (maybeService.get("battery")) {
    case 0:
        batteryLevel = 10;
        break;
    case 1:
        batteryLevel = 15;
        break;
    case 2:
        batteryLevel = 20;
        break;
    case 3:
        batteryLevel = 30;
        break;
    default:
        System.err.println("maybe label battery got choice out of range.");
        break;
}
```
