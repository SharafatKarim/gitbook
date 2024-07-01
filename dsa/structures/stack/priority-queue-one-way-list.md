# Priority Queue (one way list)

In priority queue it's just like a queue, but you have to place values with higher priority on the top of the list. Also available in STL. Read here,

{% embed url="https://www.geeksforgeeks.org/priority-queue-in-cpp-stl/" %}

And just like `queue` you can also implement manually.

## 6.13 Deletion in priority Queue

To delete we just simple delete like the previous time,

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

## 6.14 Insertion in priority queue

And for insertion, we can go ahead and implement a one way list. \
And if you want, you can also try something similar that we did in queue. In this case, we will try to use our free spaces, left in the memory!

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

## Priority Queue (one way list)

So, here's a full implementation.&#x20;

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

If it's a bit difficult, maybe you can try to do something like,

{% embed url="https://www.geeksforgeeks.org/priority-queue-set-1-introduction/" %}

But in this case it can be more time-consuming than my implementation, cause, here whenever you pop out an element you actually shift the rest.
