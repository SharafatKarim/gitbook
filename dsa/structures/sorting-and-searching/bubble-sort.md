# Bubble Sort

## Intro

In bubble, you will also compare two value per each iteration. But the difference from selection sort is that, you don't need to actually hold a value. Just go forward and scan a value with its next adjacent one!

## Code

```cpp
#include <iostream>

using namespace std;

void bubbleSort(int* arr, int size) {
    for (int i = 0; i < size - 1; i++) {
        for (int j = 0; j < size - i; j++) {
            if (arr[j] > arr[j+1]) {
                swap(arr[j], arr[j+1]);
            }
        }
    }
}

void print(int* arr, int size) {
    for (int i = 0; i < size; i++) {
        cout << arr[i] << " ";
    }
    cout << endl;
}

int main() {
    int arr[] = {5, 2, 4, 6, -1, 3};
    bubbleSort(arr, sizeof(arr)/sizeof(arr[0]));
    print(arr, sizeof(arr)/sizeof(arr[0]));
}
```
