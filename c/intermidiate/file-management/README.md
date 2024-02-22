# 💼 File management

For accessing files, we shall use `FILE`  structure in the following way,

```c
#include <stdio.h>

int main()
{
    FILE* fp;
    fp = fopen("file.txt", "w");
    fclose(fp);
    return 0;
}

```

Here, `fopen("file_path", "mode");`

`for modes,`

```markdown
a = append (creates file if not present)
w = write (creates file if not present)
a = read (error if not present)
```

***

Here, `fclose(fp)` is optional!
