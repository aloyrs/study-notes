# Searching

## Linear Search

- Check each element one by one.
- Time: O(n), Space: O(1)
- Works for unsorted arrays.
- Simple, but slow for large datasets.

## Binary Search

- Repeatedly divide sorted array in half.
- Time: O(log n), Space: O(1)
- Only works for **sorted** arrays.
- Much faster than linear search.

---

| Search | Time (Best/Worst) | Space | Sorted Required |
| ------ | ----------------- | ----- | --------------- |
| Linear | O(1) / O(n)       | O(1)  | No              |
| Binary | O(1) / O(log n)   | O(1)  | Yes             |
