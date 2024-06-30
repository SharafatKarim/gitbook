# Stack Basics

In C++ STL has stacks built in, nothing to fear!

## 6.1 Push

Insert something to the stack.

```cpp
#include<iostream>
#include <stack>

using namespace std;

void stack_push_stl() {
    stack<int> st;
    st.push(5);
    cout << st.top() << "\n";
}

int main() {
    stack_push_stl();
    return 0;
}
```

## 6.2 Pop

Delete something from the stack!

```cpp
#include<iostream>
#include <stack>

using namespace std;

void stack_pop_stl() {
    stack<int> st;
    st.push(5);
    st.push(3);
    while (!st.empty()) {
        cout << "-> " << st.top() << "\n";
        st.pop();
    }
}

int main() {
    stack_pop_stl();
    return 0;
}
```

But if you want to implement this manually like STL does?

## Stack Library

An example stack class template,

```cpp
#include <iostream>
using namespace std;
#define MAX_NUM 1000

template <typename T> class Stack {
    private:
        long long top;
        T arr[MAX_NUM];
    public:
        Stack() {top=-1;}
        T Push(T obj) {
            arr[++top] = obj;
            return arr[top];
        } long long Pop() {
            if (this ->isEmpty())
                return top;
            return --top;
        } T Peek() {
            return arr[top];
        } bool isEmpty() {
            return (top == -1);
        }
};

int main() {
    Stack<int> s;
    s.Push(5);
    cout << s.Peek() << endl;
    cout << (s.isEmpty()?"True":"False") << endl;
    s.Pop();
    cout << (s.isEmpty()?"True":"False") << endl;
    return 0;
}
```
