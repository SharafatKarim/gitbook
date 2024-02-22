# multiple character

Multiple character can be taken either using `putc and getc` or, by using `fscanf and fprintf`

Here's the method, we learned earlier by using, `putc and getc`,

```c
#include <stdio.h>

int main()
{
    FILE* fp;
    char c;

    fp = fopen("file.txt", "w"); // using write mode
    while ((c = getchar()) != EOF) // iterating until EOF
        putc(c, fp); // putting a character
    fclose(fp);

    fp = fopen("file.txt", "r"); // using read mode
    while ((c = getc(fp)) != EOF) // iterating till EOF
        printf("%c", c); // printing to our screen
    fclose(fp);

    return 0;
}

```

Here EOF is End Of File, can be triggered generally by double pressing `ctrl + d` in linux or, `ctrl + z` in windows operating system.
