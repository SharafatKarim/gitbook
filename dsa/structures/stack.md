# Stack

## RPN (Reverse Polish Notation)

Reverse Polish Notation (RPN) is a mathematical notation where every operator follows all of its operands. For instance, to add three and four, one would write "3 4 +" rather than "3 + 4". If there are multiple operations, the operator is given immediately after its second operand; so the expression written "3 − 4 + 5" would be written "3 4 − 5 +" first subtract 4 from 3, then add 5 to that.

Sample 1: Input

> 3 (a+(b_c)) ((a+b)_(z+x)) ((a+t)\*((b+(a+c))^(c+d)))

Output

> abc\*+ ab+zx+\* at+bac++cd+^\*

```cpp
#include <bits/stdc++.h>
using namespace std;

void test()
{
    string s;
    cin >> s;
    // cout << s << endl;

    stack<char> st;
    for (auto i : s)
    {
        if (i == ')')
        {
            cout << st.top();
            st.pop();
        }
        else if (i == '(')
        {
            continue;
        }
        else if ('a' <= i && i <= 'z')
        {
            cout << i;
        }
        else 
        {
            st.push(i);
        }
    }
    cout << endl;
}

int main()
{
    // your code goes here
    int t;
    cin >> t;
    while (t--)
        test();

    return 0;
}
```
