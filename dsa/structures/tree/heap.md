# Heap!

Thinking about heap sort?&#x20;

> well, you are on the right place. Let's get started!

It's another type of binary tree, just like binary seach tree. Here the root is equal or greater than it's childrens. It's also called max heap. Min heap is the vice-versa edition of it!

{% hint style="info" %}
For now we will be represing this in a linear array unlike previous two times. And yeah, in programming array's index starts from 0, but we will be storing elements from 1 index for our convenience.
{% endhint %}

## 7.9 Insertion

While inserting, we will simply add it to your linear array, and compare it with it's parent (N/2). If parent is smaller than our new node, we will go higher. In this way we will iterate, until we find our root.

```cpp
    void insert(T item) {
        if (size == MAX) {
            cout << "Heap is full\n";
            return;
        }
        size++;
        int temp = size, temp_parent;
        while (temp > 1) {
            temp_parent = temp / 2;
            if (item <= arr[temp_parent]) {
                arr[temp] = item;
                return;
            } 
            arr[temp] = arr[temp_parent];
            temp = temp_parent;
        }
        arr[temp] = item;
    }
```

## 7.10 Delete Heap

In this step, we will actually delete our topmost index.&#x20;

> Our top most index in a max heap is the highest element, right?

Here we will remove the top element and image the last element is on the top. Now we have to move our top most element (actually the last), to the appropriate place by continuously iterating.

```cpp
    T deleteMax() {
        T item = arr[1];
        T last = arr[size];
        size--;
        int temp = 1, left = 2, right = 3;
        while (right <= size) {
            if (last >= arr[left] && last >= arr[right]) {
                arr[temp] = last;
                return item;
            }
            if (arr[left] > arr[right]) {
                arr[temp] = arr[left];
                temp = left;
            } else {
                arr[temp] = arr[right];
                temp = right;
            }
            left = 2 * temp;
            right = left + 1;
        }
        if (left == size && last < arr[left]) {
            arr[temp] = arr[left];
            temp = left;
        }
        arr[temp] = last;
        return item;
    }
```

## 7.11 Heap Sort

Finally to implement heap sort, remember our top most element is the higest of the entire tree, right? So we are gonna continuously delete our top-most element and keep it in an array or process. And this should enough to get a sorted array!&#x20;

Here's the full code,

```cpp
#include <iostream>
#define MAX 100
using namespace std;

template<typename T> class Heap {
    T arr[MAX];
    int size;
public:
    Heap() {
        size = 0;
        arr[0] = -1;
    }
    void insert(T item) {
        if (size == MAX) {
            cout << "Heap is full\n";
            return;
        }
        size++;
        int temp = size, temp_parent;
        while (temp > 1) {
            temp_parent = temp / 2;
            if (item <= arr[temp_parent]) {
                arr[temp] = item;
                return;
            } 
            arr[temp] = arr[temp_parent];
            temp = temp_parent;
        }
        arr[temp] = item;
    }
    void printAll() {
        for (int i=1; i<=size; i++) {
            cout << arr[i] << " ";
        } cout << endl;
    }
    T deleteMax() {
        T item = arr[1];
        T last = arr[size];
        size--;
        int temp = 1, left = 2, right = 3;
        while (right <= size) {
            if (last >= arr[left] && last >= arr[right]) {
                arr[temp] = last;
                return item;
            }
            if (arr[left] > arr[right]) {
                arr[temp] = arr[left];
                temp = left;
            } else {
                arr[temp] = arr[right];
                temp = right;
            }
            left = 2 * temp;
            right = left + 1;
        }
        if (left == size && last < arr[left]) {
            arr[temp] = arr[left];
            temp = left;
        }
        arr[temp] = last;
        return item;
    }
};

int main() {
    int array [] = {-5, 10, 3, 1, 15, -4, 7, 1};
    Heap<int> heap;
    for (int i=0; i<6; i++) {
        heap.insert(array[i]);
    }
    heap.printAll();

    for (int i=0; i<6; i++) {
        cout << heap.deleteMax() << " ";
    } cout << endl;
    return 0;
}
```

You can go ahead and collect the sorted one in whatever way you prefer. Good luck!
