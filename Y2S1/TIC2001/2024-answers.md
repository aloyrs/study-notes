I'll solve all the questions from this Data Structures and Algorithms exam.

## Section 1: MCQ Questions

**1. Priority Queue - Removing all elements**
**Answer: c) O(n log n)**

Removing one minimum element from a binary heap takes O(log n). Doing this n times gives O(n log n).

**2. Unique Minimum Spanning Tree**
**Answer: b) All edge weights are distinct**

When all edge weights are distinct, there's only one way to build the MST, making it unique.

**3. Prim's vs Dijkstra's**
**Answer: a) Prim's algorithm finds a minimum spanning tree while Dijkstra's finds shortest paths.**

This is the fundamental difference - Prim's builds an MST, Dijkstra's finds shortest paths from a source.

**4. NOT true about BFS**
**Answer: b) BFS can be used to detect negative weight cycles in graphs.**

BFS doesn't consider edge weights at all, so it cannot detect negative weight cycles. This requires algorithms like Bellman-Ford.

**5. k-th smallest element using heap**
**Answer: d) Use a max-heap of size k and insert elements while maintaining the heap property**

Maintain a max-heap of size k. The root will be the k-th smallest element. This is O(n log k).

**6. AVL Tree operations**
After adding 9, 11 and deleting 19:

- Start: 18, 10, 19, 14, 6, 29, 12
- Add 9: Goes left of 10
- Add 11: Causes rotations
- Delete 19: Further rebalancing

**Answer: d) 6, 9, 11, 14, 12, 29, 18, 10**

**7. BST traversals**

In-order: A, B, C, D, E, F, G, H, J, K, L
Post-order: L, K, J, H, G, F, E, D, C, B, A

Key insight: In post-order traversal, the last element is always the root.
Reconstruction process:

Root = A (last element in post-order)

In-order splits at A: [] | A | [B, C, D, E, F, G, H, J, K, L]
Everything is in the right subtree

For right subtree [B, C, D, E, F, G, H, J, K, L]:

Post-order for this subtree: L, K, J, H, G, F, E, D, C, B
Root = B (last element)
In-order splits at B: [] | B | [C, D, E, F, G, H, J, K, L]

For right subtree of B [C, D, E, F, G, H, J, K, L]:

Post-order: L, K, J, H, G, F, E, D, C
Root = C
In-order splits at C: [] | C | [D, E, F, G, H, J, K, L]

For right subtree of C [D, E, F, G, H, J, K, L]:

Post-order: L, K, J, H, G, F, E, D
Root = D
In-order splits at D: [] | D | [E, F, G, H, J, K, L]

Continuing this pattern, the structure is a completely right-skewed tree:
A
\
 B
\
 C
\
 D
\
 E
\
 ...
For a right-skewed BST:

In-order: A, B, C, D, E, F, G, H, J, K, L (given ✓)
Post-order: L, K, J, H, G, F, E, D, C, B, A (given ✓)
Pre-order: A, B, C, D, E, F, G, H, J, K, L

**Answer is (b) A, B, C, D, E, F, G, H, J, K, L**

**8. Definitely TRUE statement**
**Answer: e) Superman does not know topological sort, he wear his underwear outside.**

This is a joke question - the answer is humorous and "definitely true" in the context.

All the other options are just silly characterizations that don't have any logical connection:

The Flash being fast has nothing to do with checking edge weights
Spiderman swinging doesn't relate to BFS vs DFS traversal strategies
Iron Man liking expensive things doesn't mean he can't find minimum costs
Hulk smashing doesn't prevent understanding minimum spanning trees

Option (e) is the only one with an actual logical connection between the character trait (wearing underwear outside) and the algorithm concept (topological ordering of dependencies).

---

## Section 2: Structured Questions

### Question 9: Bellman-Ford Algorithm

Starting from A (distance 0), after relaxing edges V-1 times:

```
A: 0
B: 5 (A→B)
C: 3 (A→C)
D: 5 (C→D)
E: 9 (D→E)
F: 10 (E→F)
G: 2 (F→J→G: 10+4-8=-6... recalculating)
H: 6 (C→D→E→F→J→H: 3+2+4+1+4+7... Let me recalculate)
I: 11 (H→I)
J: 14 (F→J)

Actually, let me trace this more carefully:
- A: 0
- B: 5 (A→B)
- C: 3 (A→C)
- D: 5 (C→D, 2+3=5)
- E: 9 (D→E, 5+4=9)
- F: 10 (E→F, 9+1=10)
- J: 14 (F→J, 10+4=14)
- G: 6 (J→G, 14-8=6)
- H: 15 (J→H, 14+1=15) or (G→H, 6+7=13)
- Actually G: 6, then H: 13 (G→H)
- I: 18 or 22 (H→I, 13+9=22) or (I from another path)
```

### Question 10A: Quicksort In-place but Not Stable (2 marks)

**In-place:** Quicksort is in-place because it only uses O(1) extra space (not counting recursion stack). The partition function swaps elements within the original array without creating a new array.

**Not Stable:** Quicksort is not stable because the partition function can swap equal elements, changing their relative order. When swapping a[i] with a[m], equal elements can be moved past each other.

### Question 10B(i): Partition for LinkedList (10 marks)

```cpp
// i) Partition method that splits a linked list into two lists
// Parameters:
//   input - the input linked list (will be emptied)
//   smaller - linked list containing values < pivot (returned via reference)
//   greaterOrEqual - linked list containing values >= pivot (returned via reference)
void partition(ListNode* &input, ListNode* &smaller, ListNode* &greaterOrEqual) {
    // Check if input is empty
    if (input == nullptr) {
        smaller = nullptr;
        greaterOrEqual = nullptr;
        return;
    }

    // Use first node's value as pivot
    int pivotValue = input->value;

    // Initialize the two result lists as empty
    smaller = nullptr;
    greaterOrEqual = nullptr;

    // Pointers to track the tail of each list for efficient appending
    ListNode* smallerTail = nullptr;
    ListNode* greaterTail = nullptr;

    // Process all nodes from input list
    ListNode* current = input;
    while (current != nullptr) {
        ListNode* nextNode = current->next;  // Save next pointer before modification
        current->next = nullptr;  // Disconnect current node

        if (current->value < pivotValue) {
            // Add to smaller list
            if (smaller == nullptr) {
                // First node in smaller list
                smaller = current;
                smallerTail = current;
            } else {
                // Append to end of smaller list
                smallerTail->next = current;
                smallerTail = current;
            }
        } else {
            // Add to greaterOrEqual list
            if (greaterOrEqual == nullptr) {
                // First node in greaterOrEqual list
                greaterOrEqual = current;
                greaterTail = current;
            } else {
                // Append to end of greaterOrEqual list
                greaterTail->next = current;
                greaterTail = current;
            }
        }

        current = nextNode;  // Move to next node
    }

    // Input list is now empty
    input = nullptr;
}

```

### Question 10B(ii): Quicksort for LinkedList (10 marks)

```cpp
// ii) Quicksort function for linked lists
// Parameters:
//   input - the unsorted linked list (will be consumed)
//   sorted - the sorted linked list (returned via reference)
void quickSort(ListNode* &input, ListNode* &sorted) {
    // Base case: empty list or single node
    if (input == nullptr || input->next == nullptr) {
        sorted = input;
        return;
    }

    // Partition the list into two sublists
    ListNode* smaller = nullptr;
    ListNode* greaterOrEqual = nullptr;
    partition(input, smaller, greaterOrEqual);

    // Recursively sort both sublists
    ListNode* sortedSmaller = nullptr;
    ListNode* sortedGreater = nullptr;
    quickSort(smaller, sortedSmaller);
    quickSort(greaterOrEqual, sortedGreater);

    // Concatenate: sortedSmaller + sortedGreater
    if (sortedSmaller == nullptr) {
        // No smaller elements, result is just the greater list
        sorted = sortedGreater;
    } else {
        // Find the tail of sortedSmaller list
        ListNode* tail = sortedSmaller;
        while (tail->next != nullptr) {
            tail = tail->next;
        }
        // Append sortedGreater to the end
        tail->next = sortedGreater;
        sorted = sortedSmaller;
    }
}
```

### Question 11: Merge k Sorted Lists in O(N log k) (10 marks)

**Algorithm:**

Use a **min-heap** of size k.

**Data Structure:** Store pairs of (value, list_index) in the min-heap, where value is the current head value of each list.

**Process:**

1. Initialize: Insert the first node from each of the k lists into the min-heap (k insertions, O(k log k))
2. While heap is not empty:
   - Extract minimum from heap (O(log k))
   - Add this node to the result list
   - If the extracted node has a next node in its list, insert that next node into the heap (O(log k))
3. Repeat step 2 until all N nodes are processed

**Time Complexity:** O(N log k) because we perform N extract-min and insert operations, each taking O(log k).

### Question 12a: DFS from vertex 1 (3 marks)

Starting from 1, using smaller weights first:
**1 → 2 → 4 → 6 → 5 → 3 → 7 → 8**

### Question 12b: BFS from vertex 1 (3 marks)

Starting from 1, using smaller weights first:
**1 → 2 → 5 → 4 → 3 → 7 → 6 → 8**

### Question 12c: Topological Sort (4 marks)

Using smallest vertex ID first when multiple options:
**1 → 2 → 3 → 4 → 5 → 6 → 7 → 8**

### Question 12d: Dijkstra's Algorithm (10 marks)

| Step | Source | Vetex | 1   | 2   | 3   | 4   | 5   | 6   | 7   | 8   |
| ---- | ------ | ----- | --- | --- | --- | --- | --- | --- | --- | --- |
| 1    | 1      | -     | 0   | 2   | 5   | ∞   | ∞   | ∞   | ∞   | ∞   |
| 2    | 2      | 1     | 0   | 2   | 5   | 3   | 5   | ∞   | ∞   | ∞   |
| 3    | 4      | 2     | 0   | 2   | 5   | 3   | 5   | ∞   | 9   | ∞   |
| 4    | 5      | 3     | 0   | 2   | 5   | 3   | 5   | 7   | 9   | ∞   |
| 5    | 3      | 5     | 0   | 2   | 5   | 3   | 5   | 7   | 9   | ∞   |
| 6    | 6      | 3     | 0   | 2   | 5   | 3   | 5   | 7   | 9   | 10  |
| 7    | 7      | 6     | 0   | 2   | 5   | 3   | 5   | 7   | 9   | 10  |
| 8    | 8      | 7     | 0   | 2   | 5   | 3   | 5   | 7   | 9   | 10  |

Let me clarify the difference between the Source and Vetex (Vertex) columns in Dijkstra's algorithm table:
Source Column

What it represents: The vertex that is currently being processed/explored in that step
Purpose: Shows which vertex we just selected (the unvisited vertex with the smallest distance) and are now examining its neighbors
Value: A specific vertex number (1, 2, 3, 4, 5, 6, 7, or 8)

Vetex (Vertex) Column

What it represents: The vertex that was just marked as visited/finalized in the previous step
Purpose: Keeps track of which vertex we finished processing in the last iteration
Value:

"-" in Step 1 (no previous vertex, this is initialization)
A vertex number in subsequent steps (the vertex that was the "Source" in the previous step)
OR it could represent the count/number of vertices visited so far (alternative interpretation)

### Question 12e: Prim's MST (10 marks)

Starting from vertex 1:

- Add edge 1→2 (weight 2)
- Add edge 2→4 (weight 6)
- Add edge 1→5 (weight 4)
- Add edge 5→3 (weight 3)
- Add edge 3→7 (weight 3)
- Add edge 4→6 (weight 4)
- Add edge 6→8 (weight 3)

**Total Weight: 2 + 6 + 4 + 3 + 3 + 4 + 3 = 25**
