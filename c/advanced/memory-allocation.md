# 🎑 Memory allocation

## Introduction

Memory allocation in C allows you to dynamically allocate and free memory during program execution using functions like `malloc`, `calloc`, `realloc`, and `free` from `<stdlib.h>`.

## Example: Using malloc and free

```c
#include <stdio.h>
#include <stdlib.h>

int main() {
    int *arr;
    int n = 5;
    arr = (int*)malloc(n * sizeof(int));
    if (arr == NULL) {
        printf("Memory allocation failed!\n");
        return 1;
    }
    for (int i = 0; i < n; i++) {
        arr[i] = i + 1;
    }
    for (int i = 0; i < n; i++) {
        printf("%d ", arr[i]);
    }
    free(arr);
    return 0;
}
```

