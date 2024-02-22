# Error handling

Testing a file is available or not,

```c
#include <stdio.h>

int main()
{
    FILE* fp;
    char c[16];

    fp = fopen("file1.txt", "r"); // using write mode
    if (fp == NULL)
        printf("File not found!");
    return 0;
}
```
