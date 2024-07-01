# Array and matrix

Array is the basic data structure for storing, right?\
Let's take a look,

## 4.1 Traversing

In traversing, we will visit every single element. Why?\
Well, it's up to you. For now let's print!

```cpp
#include <iostream>
using namespace std;

void traverse_1(int arr[], int lower_bound, int upper_bound) {
    int temp = lower_bound;
    while (temp <= upper_bound) {
        cout << arr[temp] << " ";
        temp++;
    }
    cout << endl;
}

void traverse_2(int arr[], int lower_bound, int upper_bound) {
    for (int i = lower_bound; i <= upper_bound; i++) {
        cout << arr[i] << " ";
    }
    cout << endl;
}

int main() {
    int arr[5] = {1, 2, 3, 4, 5};
    traverse_1(arr, 0, 4);
    traverse_2(arr, 0, 4);
}
```

## 4.2 Insertion into an array

As arrays are stored linearly, so what if I want to insert something in the middle?\
yeah! We have to shift things around!

```cpp
#include <iostream>
using namespace std;

int insert(int arr[], int n, int k, int item) {
    // for (int i = n - 1; i >= k; i--) {
    //     arr[i + 1] = arr[i];
    // }
    
    int j = n - 1;
    while (j >= k) {
        arr[j + 1] = arr[j];
        j--;
    }

    arr[k] = item;
    return n + 1;
}

void printArray(int arr[], int n) {
    for (int i=0; i < n; i++) {
        cout << arr[i] << " ";
    }
    cout << endl;
}

int main() {
    int arr[50] = {1, 2, 3, 4, 5};
    int n = 5; // number of elements in the array
    int k = 2; // position to insert a new value
    int item = 10; // value to insert

    n = insert(arr, n, k - 1, item);
    printArray(arr, n);
}
```

> Here, commented lines are the implemention of the same while logic in if logic. Hope you got that!

## 4.3 Deletion in arrays

It's just like insertion but much simpler!

```cpp
#include <iostream>
using namespace std;

int deleteElement(int arr[], int n, int k) {
    // int item = arr[k]; // for processing     
    for (int j=k; j < n-1; j++) {
        arr[j] = arr[j+1];
    }
    return n - 1;
}

void printArray(int arr[], int n) {
    for (int i=0; i < n; i++) {
        cout << arr[i] << " ";
    }
    cout << endl;
}

int main() {
    int arr[50] = {1, 2, 3, 4, 5};
    int n = 5; // number of elements in the array
    int k = 2; // position to deleteElement a new value

    n = deleteElement(arr, n, k - 1);
    printArray(arr, n);
}
```

{% hint style="info" %}
In above codes, I didn't include corner case handlers or any validators, so it's up to you. Nothing to worry much here, I guess.
{% endhint %}

## 4.4 Bubble Sort

As an example on how to do operation on array, let's sort. We will pick bubble buddy for now.

```cpp
#include <iostream>
using namespace std;

void swap(int *a, int *b) {
    int temp = *b;
    *b = *a;
    *a = temp;
}

void bubbleSort(int *arr, int n) {
    for (int i=0; i< n; i++) {
        for (int j=0; j < n-i; j++) {
            if (arr[j] > arr[j+1]) {
                swap(&arr[j], &arr[j+1]);
            }
        }
    }
}

void printArray(int *arr, int n) {
    for (int i=0; i < n; i++) {
        cout << arr[i] << " ";
    }
    cout << endl;
}

int main() {
    int arr[] = {12, 2, 39, -4, 25};
    bubbleSort(arr, sizeof(arr)/sizeof(int));
    printArray(arr, sizeof(arr)/sizeof(int));
}
```

## 4.5 Linear Search

And for searching with O(n) complexity,

```cpp
#include <iostream>
using namespace std;

int linearSearch(int arr[], int n, int item) {
    for (int i=0; i < n; i++) {
        if (arr[i] == item) {
            return i;
        }
    } // While loop? Try yourself!
    return -1;
}

int main() {
    int arr[] = {12, 2, 39, -4, 25};
    int item = 39;
    cout << linearSearch(arr, sizeof(arr)/sizeof(int), item) << endl;
}
```

## 4.6 Binary Search

Accordingly, let's divide and conquer. Get your sword ready to slice the array into half, XD.

```cpp
#include <iostream>
using namespace std;

int binarySearch(int arr[], int n, int item) {
    int lower_bound = 0;
    int upper_bound = n - 1;
    while (lower_bound <= upper_bound) {
        int mid = (lower_bound + upper_bound) / 2;
        if (arr[mid] == item) {
            return mid;
        } else if (arr[mid] < item) {
            lower_bound = mid + 1;
        } else {
            upper_bound = mid - 1;
        }
    }
    return -1;
}

int main() {
    int arr[] = {12, 2, 39, -4, 25};
    int item = 39;
    cout << binarySearch(arr, sizeof(arr)/sizeof(int), item) << endl;
}
```

## 4.7 Matrix multiplication

And how about 2D array? Let's multiply 2 matrix,

```cpp
#include <iostream>
using namespace std;

void matrixMultiplication(int matrix_a[][3], int matrix_b[][3], int M, int P, int N) {
    int matrix_c[M][N];
    for (int i=0; i < M; i++) {
        for (int j=0; j < N; j++) {
            matrix_c[i][j] = 0;
            for (int k=0; k < P; k++) {
                matrix_c[i][j] += matrix_a[i][k] * matrix_b[k][j];
            }
        }
    }
    for (int i=0; i < M; i++) {
        for (int j=0; j < N; j++) {
            cout << matrix_c[i][j] << " ";
        }
        cout << endl;
    }
}

int main() {
    int matrix_a[][3] = {{1, -2, 3}, {0, 4, 5}}; // M x P
    int matrix_b[][3] = {{3, 0, -6}, {2, -3, 1}, {2, 5, 3}}; // P x N

    matrixMultiplication(matrix_a, matrix_b, 2, 3, 3);
}
```

So, we passed an array normally to do something, but what if I want back that array?

## Pointer (2D array)

Here's the fun thing, pointer, which will pass as reference,

```cpp
#include <iostream>
using namespace std;

int** createMatrix(int row, int column) {
    int **matrix = new int*[row];
    for (int i=0; i < row; i++) {
        matrix[i] = new int[column];
    }
    return matrix;
}

void printMatrix(int **matrix, int row, int column) {
    for (int i=0; i < row; i++) {
        for (int j=0; j < column; j++) {
            cout << matrix[i][j] << " ";
        }
        cout << endl;
    }
}

void deleteMatrix(int **matrix, int row) {
    for (int i=0; i < row; i++) {
        delete[] matrix[i];
    }
    delete[] matrix;
}

void matrixMultiplication(int matrix_a[][3], int matrix_b[][3], int **matrix_c, int M, int P, int N) {
    for (int i=0; i < M; i++) {
        for (int j=0; j < N; j++) {
            matrix_c[i][j] = 0;
            for (int k=0; k < P; k++) {
                matrix_c[i][j] += matrix_a[i][k] * matrix_b[k][j];
            }
        }
    }
}

int main() {
    int matrix_a[][3] = {{1, -2, 3}, {0, 4, 5}}; // M x P
    int matrix_b[][3] = {{3, 0, -6}, {2, -3, 1}, {2, 5, 3}}; // P x N

    int **matrix_c;
    matrix_c = createMatrix(2, 3);

    matrixMultiplication(matrix_a, matrix_b, matrix_c, 2, 3, 3);
    printMatrix(matrix_c, 2, 3);
    deleteMatrix(matrix_c, 2);
}
```

In this way, we can do more than just copy. Hope it helps :).
