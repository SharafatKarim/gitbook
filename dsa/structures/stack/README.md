# Stack & Queue

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
