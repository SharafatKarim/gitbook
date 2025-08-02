# ⚛ Data type

## Introduction

In C, data types specify the type of data that a variable can store. Common data types include:

- `int` : Integer numbers
- `float` : Floating-point numbers
- `char` : Characters
- `double` : Double-precision floating-point numbers

## Example: Declaring Variables of Different Data Types

```c
#include <stdio.h>

int main() {
    int age = 20;
    float weight = 65.5;
    char grade = 'A';
    double balance = 12345.67;
    printf("Age: %d\n", age);
    printf("Weight: %.1f\n", weight);
    printf("Grade: %c\n", grade);
    printf("Balance: %.2lf\n", balance);
    return 0;
}
```

