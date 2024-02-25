# Big integer

A big integer is an integer with arbitrary precision. It can store numbers with a large number of digits. It is useful when we need to store large numbers that cannot be stored in the standard data types like `int` or `long long`.

A problem to add two numbers,

```cpp
#include <bits/stdc++.h>
using namespace std;

// Simple template by sharafat
typedef long long ll;
typedef vector<ll> vl;

#define endl '\n'

void print(vl a)
{
    for (auto i : a)
    {
        cout << i ;
    }
    cout << endl;
}

void add(vl a, vl b)
{
    reverse(a.begin(), a.end());
    reverse(b.begin(), b.end());

    vl max_arr;
    if (a.size() > b.size()) max_arr = a; else max_arr = b;

    ll len = min(a.size(), b.size());
    ll max_len = max(a.size(), b.size());
    vl s;
    ll c = 0;
    for (ll i = 0; i < len; i++)
    {
        ll t = a[i]+b[i]+c;
        s.emplace_back(t % 10);
        c = t / 10;
    }
    for (ll i = len; i < max_len; i++)
    {
        ll t = max_arr[i]+c;
        s.emplace_back(t % 10);
        c = t / 10;
    }
    if (c) s.emplace_back(c);
    reverse(s.begin(), s.end());
    print(s);
}

int main()
{
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    // Code starts here

    ll t;
    cin >> t;
    while (t--)
    {
        string a, b;
        cin >> a >> b;

        vl s, d;

        for (int i = 0; i < a.size(); i++)
        {
            s.emplace_back(a[i] - '0');
            // s[i] = a[i] - '0';
        }
        for (int i = 0; i < b.size(); i++)
        {
            d.emplace_back(b[i] - '0');
            // d[i] = b[i] - '0';
        }

        add(s, d);
    }

    // Code ends here
    return 0;
}
```