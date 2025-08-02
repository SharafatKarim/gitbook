# 📽 Preprocessor

## Introduction

The C preprocessor handles directives that begin with `#`, such as `#include`, `#define`, and `#ifdef`. These are processed before actual compilation.

## Example: Using #define and #include

```c
#include <stdio.h>
#define PI 3.14159

int main() {
    printf("Value of PI: %f\n", PI);
    return 0;
}
```

