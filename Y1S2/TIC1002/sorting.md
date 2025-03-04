<<<<<<< HEAD
# Sorting

## Selection Sort

- Find the smallest element and swap it to the front.
- Time: O(n²), Space: O(1)
- In-place, not stable.

## Insertion Sort

- Build sorted list by inserting each element into the correct position.
- Time: O(n²), Space: O(1)
- In-place, stable.
- Good for nearly sorted data.

## Bubble Sort

- Repeatedly swap adjacent elements if they are in the wrong order.
- Time: O(n²), Space: O(1)
- In-place, stable.
- Rarely used in practice.

## Merge Sort

- Divide array into halves, recursively sort, then merge.
- Time: O(n log n), Space: O(n)
- Not in-place, stable.
- Good for large datasets.

## Counting Sort

- Count occurrences, then place elements directly.
- Time: O(n + k), Space: O(n + k)
- Not comparison-based, stable.
- Works only for integers in a small range.

```cpp
#include <iostream>
#include <vector>
#include <algorithm>  // for max_element
using namespace std;

// Selection Sort
void selectionSort(vector<int>& arr) {
    int n = arr.size();
    for (int i = 0; i < n - 1; i++) {
        int minIdx = i;
        for (int j = i + 1; j < n; j++)
            if (arr[j] < arr[minIdx])
                minIdx = j;
        swap(arr[i], arr[minIdx]);
    }
}

// Insertion Sort
void insertionSort(vector<int>& arr) {
    int n = arr.size();
    for (int i = 1; i < n; i++) {
        int key = arr[i];
        int j = i - 1;
        while (j >= 0 && arr[j] > key) {
            arr[j + 1] = arr[j];
            j--;
        }
        arr[j + 1] = key;
    }
}

// Bubble Sort
void bubbleSort(vector<int>& arr) {
    int n = arr.size();
    for (int i = 0; i < n - 1; i++) {
        bool swapped = false;
        for (int j = 0; j < n - 1 - i; j++) {
            if (arr[j] > arr[j + 1]) {
                swap(arr[j], arr[j + 1]);
                swapped = true;
            }
        }
        if (!swapped) break;  // Optimization if array is already sorted
    }
}

// Merge Sort (Helper + Sort Function)
void merge(vector<int>& arr, int l, int m, int r) {
    vector<int> left(arr.begin() + l, arr.begin() + m + 1);
    vector<int> right(arr.begin() + m + 1, arr.begin() + r + 1);

    int i = 0, j = 0, k = l;
    while (i < left.size() && j < right.size())
        arr[k++] = (left[i] <= right[j]) ? left[i++] : right[j++];
    while (i < left.size())
        arr[k++] = left[i++];
    while (j < right.size())
        arr[k++] = right[j++];
}

void mergeSort(vector<int>& arr, int l, int r) {
    if (l >= r) return;
    int m = l + (r - l) / 2;
    mergeSort(arr, l, m);
    mergeSort(arr, m + 1, r);
    merge(arr, l, m, r);
}

// Counting Sort
void countingSort(vector<int>& arr) {
    int maxVal = *max_element(arr.begin(), arr.end());
    vector<int> count(maxVal + 1, 0);

    // Count occurrences
    for (int num : arr) count[num]++;

    // Overwrite array with sorted order
    int idx = 0;
    for (int num = 0; num <= maxVal; num++) {
        while (count[num]--) {
            arr[idx++] = num;
        }
    }
}

// Utility to print array
void printArray(const vector<int>& arr) {
    for (int x : arr) cout << x << " ";
    cout << endl;
}

// Example usage
int main() {
    vector<int> arr = {5, 3, 8, 6, 2, 7, 4, 1};

    cout << "Original Array: ";
    printArray(arr);

    // Run each sort and print results
    vector<int> temp = arr;

    selectionSort(temp);
    cout << "Selection Sort: ";
    printArray(temp);

    temp = arr;
    insertionSort(temp);
    cout << "Insertion Sort: ";
    printArray(temp);

    temp = arr;
    bubbleSort(temp);
    cout << "Bubble Sort: ";
    printArray(temp);

    temp = arr;
    mergeSort(temp, 0, temp.size() - 1);
    cout << "Merge Sort: ";
    printArray(temp);

    temp = arr;
    countingSort(temp);
    cout << "Counting Sort: ";
    printArray(temp);

    return 0;
}

```

| Sort      | Time (Best/Worst) | Space    | Stable | In-Place |
| --------- | ----------------- | -------- | ------ | -------- |
| Selection | O(n²) / O(n²)     | O(1)     | No     | Yes      |
| Insertion | O(n) / O(n²)      | O(1)     | Yes    | Yes      |
| Bubble    | O(n) / O(n²)      | O(1)     | Yes    | Yes      |
| Merge     | O(n log n)        | O(n)     | Yes    | No       |
| Counting  | O(n + k)          | O(n + k) | Yes    | No       |
=======
# Selection sort

- O(n^2)
- loops through to find the smallest/largest to form sorted sub-array on left/right respectively
- loop through remaining till array is sorted

# Bubble sort

- Look at two elements and compare the values , if left > right then swap , keep swapping until the largest is on the right (largest bubbles up to the right)

- the right side forms a sorted sub-array, repeat until all large values bubble up to the right , array will be sorted small to large

# Insertion sort

- Start from left , assume first element in array is sorted.
- Work from left to right from index 1 to check if it is in the right place in accordance to the sorted array (if its smaller then swap with values in sorted array to find its place)
- Keep looping until each value is in the sorted array, array will be sorted smallest to largest

# Counting sort
>>>>>>> 725f057d90aec9adee5d679ce5a5ad4339751830
