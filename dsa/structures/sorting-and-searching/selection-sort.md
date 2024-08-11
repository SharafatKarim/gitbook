# Selection Sort

## Intro

In selection, you will also iterate. But the difference is, you will hold each value and compare the rest alongside it! If you find a smaller value, you can swap.

## Code

```cpp
#include <iostream>

using namespace std;

void selectionSort(int* arr, int size) {
    for (int i = 0; i < size - 1; i++) {
        for (int j = i + 1; j < size; j++) {
            if (arr[j] < arr[i]) {
                swap(arr[j], arr[i]);
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
    int arr[] = {5, 2, 4, 6, 1, 3};
    selectionSort(arr, sizeof(arr)/sizeof(arr[0]));
    print(arr, sizeof(arr)/sizeof(arr[0]));
}
```
