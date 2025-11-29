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
Given in-order: A, B, C, D, E, F, G, H, J, K, L
Given post-order: L, K, J, H, G, F, E, D, C, B, A

From post-order, the root is A. From in-order, everything is to the right of A.

**Answer: d) A, B, C, L, D, K, E, J, F, H, G**

**8. Definitely TRUE statement**
**Answer: e) Superman does not know topological sort, he wear his underwear outside.**

This is a joke question - the answer is humorous and "definitely true" in the context.

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
void partition(ListNode* &input, ListNode* &less, ListNode* &greaterOrEqual) {
    if (input == nullptr) {
        less = nullptr;
        greaterOrEqual = nullptr;
        return;
    }
    
    int pivot = input->value;
    ListNode* lessTail = nullptr;
    ListNode* geTail = nullptr;
    less = nullptr;
    greaterOrEqual = nullptr;
    
    ListNode* current = input->next; // Skip pivot
    ListNode* pivotNode = input;
    pivotNode->next = nullptr;
    
    while (current != nullptr) {
        ListNode* nextNode = current->next;
        current->next = nullptr;
        
        if (current->value < pivot) {
            if (less == nullptr) {
                less = current;
                lessTail = current;
            } else {
                lessTail->next = current;
                lessTail = current;
            }
        } else {
            if (greaterOrEqual == nullptr) {
                greaterOrEqual = current;
                geTail = current;
            } else {
                geTail->next = current;
                geTail = current;
            }
        }
        current = nextNode;
    }
    
    // Add pivot to greaterOrEqual list
    if (greaterOrEqual == nullptr) {
        greaterOrEqual = pivotNode;
    } else {
        geTail->next = pivotNode;
    }
}
```

### Question 10B(ii): Quicksort for LinkedList (10 marks)

```cpp
void quickSort(ListNode* &input, ListNode* &sorted) {
    if (input == nullptr || input->next == nullptr) {
        sorted = input;
        return;
    }
    
    ListNode* less = nullptr;
    ListNode* greaterOrEqual = nullptr;
    
    partition(input, less, greaterOrEqual);
    
    ListNode* sortedLess = nullptr;
    ListNode* sortedGE = nullptr;
    
    quickSort(less, sortedLess);
    quickSort(greaterOrEqual, sortedGE);
    
    // Merge: sortedLess + sortedGE
    if (sortedLess == nullptr) {
        sorted = sortedGE;
    } else {
        sorted = sortedLess;
        ListNode* tail = sortedLess;
        while (tail->next != nullptr) {
            tail = tail->next;
        }
        tail->next = sortedGE;
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

| Step | Source | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 |
|------|--------|---|---|---|---|---|---|---|---|
| 1 | 1 | 0 | 2 | 5 | ∞ | ∞ | ∞ | ∞ | ∞ |
| 2 | 2 | 0 | 2 | 5 | 8 | ∞ | ∞ | ∞ | ∞ |
| 3 | 3 | 0 | 2 | 5 | 8 | 8 | ∞ | 8 | ∞ |
| 4 | 5 | 0 | 2 | 5 | 8 | 8 | 14 | 8 | ∞ |
| 5 | 7 | 0 | 2 | 5 | 8 | 8 | 14 | 8 | 16 |
| 6 | 4 | 0 | 2 | 5 | 8 | 8 | 12 | 8 | 16 |
| 7 | 6 | 0 | 2 | 5 | 8 | 8 | 12 | 8 | 15 |
| 8 | 8 | 0 | 2 | 5 | 8 | 8 | 12 | 8 | 15 |

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