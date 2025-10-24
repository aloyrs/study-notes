## Summary of Sorting Algorithms and Concepts

### Comparison-Based and Iterative Algorithms

1.  **Selection Sort**
    * **Description:** An iterative, comparison-based algorithm that repeatedly finds the **minimum** element from the unsorted portion of the array and places it at the beginning. It makes one swap per pass.
    * **Time Complexity:** $O(n^2)$ (Worst, Average, Best)
    * **Space Complexity:** $O(1)$ (In-place)

2.  **Bubble Sort**
    * **Description:** An iterative, comparison-based algorithm that repeatedly steps through the list, compares **adjacent elements**, and swaps them if they are in the wrong order, causing the largest elements to "bubble up" to their correct positions.
    * **Time Complexity:** $O(n^2)$ (Worst, Average), $O(n)$ (Best, if already sorted)
    * **Space Complexity:** $O(1)$ (In-place)

3.  **Insertion Sort**
    * **Description:** An iterative, comparison-based algorithm that builds the final sorted array one item at a time. It iterates through the input elements and **inserts** each element into its correct position among the already sorted elements.
    * **Time Complexity:** $O(n^2)$ (Worst, Average), $O(n)$ (Best, if already sorted)
    * **Space Complexity:** $O(1)$ (In-place)

### Comparison-Based and Recursive Algorithms

4.  **Merge Sort**
    * **Description:** A recursive, comparison-based algorithm that follows the **Divide and Conquer** paradigm. It recursively divides the array into two halves, sorts them independently, and then **merges** the two sorted halves to produce the final result.
    * **Time Complexity:** $O(n \log n)$ (Worst, Average, Best)
    * **Space Complexity:** $O(n)$ (Requires auxiliary space for merging)

5.  **Quick Sort**
    * **Description:** A recursive, comparison-based algorithm also following the **Divide and Conquer** paradigm. It selects an element as a **pivot** and partitions the other elements into two sub-arrays, according to whether they are less than or greater than the pivot. It then recursively sorts the sub-arrays.
    * **Time Complexity:** $O(n^2)$ (Worst, if pivot selection is poor), $O(n \log n)$ (Average, Best)
    * **Space Complexity:** $O(\log n)$ (Auxiliary space for recursion stack)

### Non-Comparison Based

6.  **Radix Sort**
    * **Description:** A non-comparison based algorithm that sorts integers by processing individual **digits** (or bits). It typically uses an intermediate stable sort (like Counting Sort) to sort the elements based on each digit, from least significant to most significant.
    * **Time Complexity:** $O(d(n+b))$ (where $d$ is the number of digits and $b$ is the base)
    * **Space Complexity:** $O(n+b)$ (Required for auxiliary counting/bucket arrays)

### Comparison of Sort Algorithms and Concepts

7.  **Comparison of Sort Algorithms**
    * **In-place sort:** An algorithm that sorts the data using only a small, constant amount of **extra** memory (e.g., $O(1)$ or $O(\log n)$ auxiliary space). Examples include Selection Sort, Bubble Sort, Insertion Sort, and Quick Sort.
    * **Stable sort:** An algorithm that preserves the **relative order of equal elements** from the input to the output. If two elements are equal, their order remains the same after sorting. Examples include Merge Sort, Insertion Sort, and Bubble Sort.

### STL Implementation

8.  **$\text{std::sort()}$ in C++ STL**
    * **Description:** The C++ Standard Library's $\text{std::sort()}$ is implemented using **IntroSort**, which is a hybrid algorithm. It starts with **Quick Sort** for good average performance, switches to **Heap Sort** to guarantee $O(n \log n)$ worst-case complexity, and uses **Insertion Sort** for small partitions.
    * **Time Complexity:** $O(n \log n)$ (Guaranteed)
    * **Space Complexity:** $O(\log n)$ (Auxiliary space for recursion stack)
    * **Note:** $\text{std::sort()}$ is typically **not stable**. $\text{std::stable\_sort()}$ is used when stability is required.