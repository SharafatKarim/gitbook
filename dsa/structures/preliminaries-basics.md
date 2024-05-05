# Preliminaries (basics)

## 2.1 Largest element in array

Using `goto` with c++,

```cpp
#include <iostream>
using namespace std;

void LargestElementInArray(int DATA[], int N)
{
    int K = 0, LOC = 0, MAX = DATA[0];
increment_counter:
    K = K + 1;
    if (K == N)
    {
        cout << "LOC = " << LOC << ", MAX = " << MAX << "\n";
        return;
    }
    if (MAX < DATA[K])
    {
        LOC = K;
        MAX = DATA[K];
    }
    goto increment_counter;
}

int main()
{
    int DATA[] = {3, 5, 9, 2};
    int N = sizeof(DATA) / sizeof(int);
    LargestElementInArray(DATA, N);
    return 0;
}
```

## 2.2 Quadratic equation

```cpp
#include <iostream>
#include <math.h>
using namespace std;

int main()
{
    int A, B, C;
    cin >> A >> B >> C;
    int D = B * B - 4 * A * C;
    if (D > 0)
    {
        float X1 = (-B + sqrt(D)) / (2 * A);
        float X2 = (-B - sqrt(D)) / (2 * A);
        cout << X1 << " and " << X2 << "\n";
    }
    else if (D == 0)
    {
        float X = -B / 2 * A;
        cout << "UNIQUE SOLUTION : " << X << "\n";
    }
    else 
    {
        cout << "NO REAL SOLUTIONS" << "\n";
    }
    return 0;
}
```

## 2.3 Largest element in array (while loop)

```cpp
#include <iostream>
using namespace std;

void LargestElementInArray(int DATA[], int N)
{
    int K = 0, LOC = 0, MAX = DATA[0];
    while (K < N)
    {
        if (MAX < DATA[K])
        {
            LOC = K;
            MAX = DATA[K];
        }
        K = K + 1;
    }
    cout << "LOC = " << LOC << ", MAX = " << MAX << "\n";
}

int main()
{
    int DATA[] = {3, 5, 9, 2};
    int N = sizeof(DATA) / sizeof(int);
    LargestElementInArray(DATA, N);
    return 0;
}

```

Same code as 2.1 but this time with while loop. Steps are as described as DS textbook (SEYMOUR LIPSCHUTZ)

## 2.4 Linear search

```cpp
#include <iostream>
using namespace std;

void LinearSearch(int DATA[], int N, int ITEM)
{
    int K = 0, LOC = -1;
    while (LOC == -1 && K < N)
    {
        if (ITEM == DATA[K])
            LOC = K;
        K = K + 1;
    }
    if (LOC == -1)
        cout << "ITEM is not on the array DATA\n";
    else
        cout << LOC << " is the location of ITEM\n";
    return;
}

int main()
{
    int DATA[] = {3, 5, 9, 2};
    int N = sizeof(DATA) / sizeof(int);
    int ITEM = 9;
    LinearSearch(DATA, N, ITEM);
    return 0;
}
```
