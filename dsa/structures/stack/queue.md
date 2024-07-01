# Queue

Just like `stack` I hope you can go ahead and implement queue like you did stack with STL in c++. For reference, just use your favorite search engine.&#x20;

So here's an implementation of queue with class,

## 6.11 Insertion of queue

In the insertion method,  suppose you have total 3 space. And there's an element on 3 but not 1 and 2. So if you just simply use a linked list then, you will have overflow error. But you can actually utilize that 1 and 2 space. Here's the implementation,

```cpp
int insert(T item) {
        if ((front == 0 && rear == MAX_NUM - 1) || (front == rear + 1)) {
            cout << "OVERFLOW!\n";
            return -1;
        } 
        if (front == -1) {
            front = 0;
            rear = 0;
        } else if (rear == MAX_NUM - 1) {
            rear = 0;
        } else {
            rear++;
        }
        arr[rear] = item;
        return rear;
    }
```

## 6.12 Deletion of queue

```cpp
T pop() {
        if (front == -1) {
            cout << "UNDERFLOW!\n";
            return (T)0;
        }
        T item = arr[front];
        if (front == rear) 
            front = -1, rear = -1;
        else if (front == MAX_NUM - 1)
            front = 0;
        else
            front++;
        return item;
    }
```

And finally the full queue template

## Queue (full code)

```cpp
#include <iostream>
using namespace std;
#define MAX_NUM 3

template <typename T> class queue
{
private:
    long long front;
    long long rear;
    T arr[MAX_NUM];
public:
    queue() {
        front = -1;
        rear = -1;
    }
    int insert(T item) {
        if ((front == 0 && rear == MAX_NUM - 1) || (front == rear + 1)) {
            cout << "OVERFLOW!\n";
            return -1;
        } 
        if (front == -1) {
            front = 0;
            rear = 0;
        } else if (rear == MAX_NUM - 1) {
            rear = 0;
        } else {
            rear++;
        }
        arr[rear] = item;
        return rear;
    }
    T pop() {
        if (front == -1) {
            cout << "UNDERFLOW!\n";
            return (T)0;
        }
        T item = arr[front];
        if (front == rear) 
            front = -1, rear = -1;
        else if (front == MAX_NUM - 1)
            front = 0;
        else
            front++;
        return item;
    }
    T peek() {
        return arr[front];
    }
    T back() {
        return arr[rear];
    }
};

int main() {
    queue<int> data;
    data.insert(1);
    data.insert(2);
    data.insert(3);
    data.pop();
    data.insert(4); // front 1, rear 0
    data.insert(5);
    cout << data.peek();
    cout << data.back();
    return 0;
}
```

