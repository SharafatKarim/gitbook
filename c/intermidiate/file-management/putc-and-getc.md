# putc and getc

Putc (print to file)   - single character

Getc (get from file) - single character

***

```c
#include <stdio.h>

int main()
{
    FILE* fp;

    fp = fopen("file.txt", "w"); // using write mode
    putc('s', fp); // putting a character
    fclose(fp);

    fp = fopen("file.txt", "r"); // using read mode
    char c;
    c = getc(fp); // getting the character from file
    printf("%c\n", c); // printing to our screen
    fclose(fp);

    return 0;
}
```
