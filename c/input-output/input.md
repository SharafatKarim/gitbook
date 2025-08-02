# ✍ Input

## Introduction

In C, you can take input from the user using the `scanf` function.

### Example: Taking Integer Input

```c
#include <stdio.h>

int main() {
    int number;
    printf("Enter a number: ");
    scanf("%d", &number);
    printf("You entered: %d\n", number);
    return 0;
}
```

## Taking full Line Input

### Example: Taking String Input

```c
#include <stdio.h>

int main() {
    char str[100];
    printf("Enter a string: ");
    scanf("%[^\n]", str);
    printf("You entered: %s\n", str);
    return 0;
}
```
