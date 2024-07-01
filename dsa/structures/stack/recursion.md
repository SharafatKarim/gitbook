# Recursion

As we know recursion, the situation where a function is caleed from inside of that function right?

Let's have some examples,

## 6.7 Factorial

```cpp
#include<iostream>
using namespace std;

int factorialWithLoop(int n) {
    if (n == 0) return 1;
    int fact = 1;
    for (int i=1; i <= n; i++) {
        fact *= i;
    } return fact;
}

int factorialWithRecursion(int n) {
    if (n == 0) return 1;
    return n * factorialWithRecursion(n-1);
}

int main() {
    int n = 4;
    cout << factorialWithLoop(n) << "\n";
    cout << factorialWithRecursion(n) << "\n";
}
```

Here both, with and without recursion, trick is shown. Let's have an another one,

## 6.8 Fibonacci series

The trick will return the value at that place, (don't get confused with sum of Fibonacci series)

```cpp
#include<iostream>
using namespace std;

int fibonacciSeries(int n) {
    // This function will return the n'th value of the fibonacci series
    if (n == 0 || n == 1) return n;
    return fibonacciSeries(n-1) + fibonacciSeries(n-2);
}

int main() {
    int n = 10;
    cout << fibonacciSeries(n) << "\n";
}
```
