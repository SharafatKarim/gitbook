# Tower of Hanoi

An interesting game right?

If you don't know about this game, take a look here,

{% embed url="https://www.mathsisfun.com/games/towerofhanoi.html" %}
just play and learn
{% endembed %}

So to solve it (displaying the steps), carefully analyze what actually happens when you have one and two disks. Then try to recreate the scenario with 3 disks. Maybe you can find a recursive approach here, here's the code,

## 6.9 Tower of Hanoi (Recursion)

```cpp
#include<iostream>
using namespace std;

void towerOfHanoi(int n, char beg, char aux, char end) {
    if (n==1) {
        cout << beg << " -> " << end << "\n";
        return;
    }
    towerOfHanoi(n-1, beg, end, aux);
    towerOfHanoi(1, beg, aux, end);
    towerOfHanoi(n-1, aux, beg, end);
}

int main() {
    towerOfHanoi(4, 'A', 'B', 'C');
}
```

So, with recursion it's too short and feels simple right?&#x20;

It's not this simple if you want to apply this thing with stack instead of recusion. A bit of trial and error perhaps?

## 6.10 Tower of Hanoi (Stack)

It's the iterative approach of the above code with stack,

```cpp
#include<iostream>
#include<stack>
using namespace std;

void towerOfHanoi(int n, char beg, char aux, char end) {
    int add = 2;
    stack<char> st_beg, st_aux, st_end;
    stack<int> st_n, st_add;
    
    while (true) {
        if (n == 1) {
            cout << beg << " -> " << end << "\n";
            add = 5;
        }
        if (add == 2) {
            st_beg.push(beg), st_aux.push(aux), st_end.push(end);
            st_n.push(n), st_add.push(3);
            beg = st_beg.top();
            aux = st_end.top();
            end = st_aux.top();
            n--;
        }
        if (add == 3) {
            cout << beg << " -> " << end << "\n";
            st_beg.push(beg), st_aux.push(aux), st_end.push(end);
            st_n.push(n), st_add.push(5);
            beg = st_aux.top();
            aux = st_beg.top();
            end = st_end.top();
            n--;
            add = 2;
        }
        if (add == 5) {
            if (st_beg.empty()) return;
            beg = st_beg.top();
            aux = st_aux.top();
            end = st_end.top();
            n = st_n.top();
            add = st_add.top();
            st_beg.pop(), st_aux.pop(), st_end.pop(); 
            st_add.pop(), st_n.pop();
        }
    }
}

int main() {
    towerOfHanoi(3, 'A', 'B', 'C');
}
```
