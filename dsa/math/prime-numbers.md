# Primes

Two method to determine prime numbers. One is to check if a number is prime, and the other is to generate a list of prime numbers.

```cpp
#include <bits/stdc++.h>
using namespace std;

bool isPrime(long long n) {
    if (n <= 1) return false;
    if (n % 2 == 0) return false;

    int limit = sqrt(n+1);
    for (int i=3; i < limit; i += 2) {
        if (n%i==0) return false;
    }
    return true;
}

vector<bool> prime(1e5, true); // 1 = prime
void sieve(long long n) { // Sieve of Eratoshtehnes
    prime[1] = false;
    for (long long i = 2 ; i < n; i += 2) prime[i] = false;
    
    int limit = sqrt(n+1);
    for (int i=2; i < limit; i++) {
        if (prime[i]) {
            for (int j=i*i; j < limit;j += i) {
                prime[j] = false;
            }
        }
    }
}

int main() {
    sieve(1e4);
    
    cout << isPrime(35);
    cout << prime[35];
}
```
