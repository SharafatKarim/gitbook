# fprintf and fscanf

just like printf() and scanf() but for file operations!

```c
#include <stdio.h>

int main()
{
    FILE* fp;
    char c[16];

    fp = fopen("file.txt", "w"); // using write mode
    fscanf(stdin, "%s", c); // scan from stdin (standard input)
    fprintf(fp, "%s", c); // writing to file
    fclose(fp);

    fp = fopen("file.txt", "r"); // using read mode
    fscanf(fp, "%s", c); // reading from file
    fprintf(stdout, "%s", c); // printing to stdout (standard output)
    fclose(fp);

    return 0;
}
```

Here, fscanf(stdin,\*,\*) is as same as scanf(\*,\*)

***

Here's an another program to filter even and odd numbers and seperate them,

First, let's generate from 0 to 99,

```c
#include <stdio.h>
#include <string.h>
int main()
{
    FILE* fp;
    fp = fopen("input.txt", "w");
    for (int i = 0; i < 100; i++) {
        fprintf(fp, "%d\n", i);
    }
    fclose(fp);
}

```

Now, let's seperate,

```c
#include <stdio.h>
#include <string.h>
int main()
{
    FILE *fp, *f_even, *f_odd;
    fp = fopen("input.txt", "r");
    f_even = fopen("even.txt", "w");
    f_odd = fopen("odd.txt", "w");
    int i;
    while (1) {
        if (feof(fp)) {
            break;
        }
        fscanf(fp, "%d\n", &i);
        if (i % 2 == 0)
            fprintf(f_even, "%d\n", i);
        else
            fprintf(f_odd, "%d\n", i);
    }
    fclose(fp);
    return 0;
}
```
