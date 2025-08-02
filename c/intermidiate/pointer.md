# 📌 Pointer

## Introduction

A pointer in C is a variable that stores the memory address of another variable. Pointers are powerful for dynamic memory, arrays, and functions.

## Example: Pointer Declaration and Usage

```c
#include <stdio.h>

int main() {
    int num = 10;
    int *ptr = &num;
    printf("Value of num: %d\n", num);
    printf("Address of num: %p\n", (void*)&num);
    printf("Value stored in ptr: %p\n", (void*)ptr);
    printf("Value pointed by ptr: %d\n", *ptr);
    return 0;
}
```

