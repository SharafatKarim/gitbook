# 🏨 Structure

## Introduction

A structure in C is a user-defined data type that allows grouping variables of different types under a single name.

## Example: Defining and Using a Structure

```c
#include <stdio.h>

struct Person {
    char name[50];
    int age;
};

int main() {
    struct Person person1 = {"Alice", 25};
    printf("Name: %s\n", person1.name);
    printf("Age: %d\n", person1.age);
    return 0;
}
```

