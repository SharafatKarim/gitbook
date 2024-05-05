# String Processing

## 3.1 Delation

Let's start with some string processing algorithms. The first string processing algorithm is deletion. I'm not actually writin codes for finding the index and deleting the character at that index with user functions. I'm just using the built-in functions of the string class. Feel free to write your own functions.

```cpp
#include<iostream>
using namespace std;

int main()
{
    // this algorithm deletes every occurrence of pattern from str
    string str = "To be or not 2B, that is the ?";
    string pattern = "B,";

    int index = str.find(pattern);
    while (index != -1)
    {
        str.erase(index, pattern.length());
        index = str.find(pattern);
    }

    cout << str << endl;    
}
```

## 3.2 Replacement

The next string processing algorithm is replacement. This algorithm replaces every occurrence of a pattern with another pattern. Again, I'm using the built-in functions of the string class.

```cpp
#include<iostream>
using namespace std;

int main()
{
    // this algorithm replaces every occurrence of pattern from str with placeholder
    string str = "To be or not 2B, that is the ? that is 2B decided for future!";
    string pattern = "2B";
    string placeholder = "to be";

    int index = str.find(pattern);
    while (index != -1)
    {
        str.replace(index, pattern.length(), placeholder);
        index = str.find(pattern);
    }

    cout << str << endl;    
}
```

## 3.3 Pattern Matching

Pattern matching is the process of checking whether a given sequence of characters (pattern) is present in a given string or not. The simplest way to do this is to check each substring of the string with the pattern. If the substring matches the pattern, then return the index of the substring in the string. Otherwise, return -1.

```cpp
#include <iostream>
using namespace std;

int patternMatching(string str, int str_len, string pattern, int pattern_len)
{
    if (pattern_len > str_len)
        return -1;

    int k = 0, max = str_len - pattern_len + 1;
    while (k < max)
    {
        for (int l = 0; l < pattern_len; l++)
        {
            if (pattern[l] != str[l + k])
                break;
            if (l + 1 == pattern_len)
                return k;
        }
        k++;
    }
    return -1;
}

int main()
{
    string str = "To be or not 2B, that is the ?";
    string pattern = "B,";
    int index = patternMatching(str, str.length(), pattern, pattern.length());
    cout << "Index is : " << index << endl;
    return 0;
}
```

We will be using this code for the next few sections, I guess.
