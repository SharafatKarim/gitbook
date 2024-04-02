# GCD and LCM

Euclid's method should do the trick efficiently,

```cpp
#include <bits/stdc++.h>
using namespace std;

int gcd(int a, int b) {
    if (b == 0) return a;
    if (a % b == 0) return b;
    return gcd(b, a%b);
}

int lcm(int a, int b) {
    return (int)((a * b) / gcd(a, b));
}

int main() {
    cout << lcm(2, 6);
}
```
