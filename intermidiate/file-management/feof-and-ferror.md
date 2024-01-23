# feof and ferror

feof    = f + EOF (End of File)

ferror = f + error (during the reading process)

***

returns non-zero if error exists!

Here's a sample program,

```c
#include <stdio.h>

int main()
{
    FILE* fp;
    char c[16];
    fp = fopen("file.txt", "w");
    for (int i = 0; i < 10; i++)
        putc('a', fp);
    fclose(fp);

    fp = fopen("file.txt", "r");
    if (fp == NULL)
        printf("File not found!");
    char n;

    while (n = getc(fp)) {
        if (feof(fp)) {
            printf("\nRan out of data");
            break;
        }
        printf("%c\t", n);
    }
    return 0;
}

```
