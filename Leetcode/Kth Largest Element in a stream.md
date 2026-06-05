# Kth Largest Element in a Stream

**Difficulty:** Easy  
**Topic:** Heap, Binary Search, Data Structures

---

## Problem

You are part of a university admissions office and need to keep track of the kth highest test score from applicants in real-time. This helps to determine cut-off marks for interviews and admissions dynamically as new applicants submit their scores.

Implement the `KthLargest` class:

- `KthLargest(int k, int[] nums)` — Initializes the object with the integer `k` and the stream of test scores `nums`.
- `int add(int val)` — Adds a new test score `val` to the stream and returns the kth largest element in the pool of test scores so far.

---

## Approach

- Maintain a sorted list of all scores seen so far.
- On initialization, add all `nums` to the list and sort it.
- On `add`: use **binary search** (`getIndex`) to find the correct insertion position for `val`, insert it to keep the list sorted, then return the element at index `size - k` (kth largest from the end).

**Time Complexity:** O(n) per `add` due to list insertion shifting; O(log n) for the binary search  
**Space Complexity:** O(n)

---

## Code (Java)

```java
class KthLargest {
    int k;
    List<Integer> ls;

    public KthLargest(int k, int[] nums) {
        this.k = k;
        this.ls = new ArrayList<Integer>(nums.length);
        for (int it : nums) {
            ls.add(it);
        }
        Collections.sort(ls);
    }

    public int add(int val) {
        int index = getIndex(val);
        ls.add(index, val);
        return ls.get(ls.size() - k);
    }

    private int getIndex(int val) {
        int left = 0;
        int right = ls.size() - 1;
        while (left <= right) {
            int mid = (left + right) / 2;
            if (ls.get(mid) == val)
                return mid;
            if (ls.get(mid) < val)
                left = mid + 1;
            else
                right = mid - 1;
        }
        return left;
    }
}

/**
 * Your KthLargest object will be instantiated and called as such:
 * KthLargest obj = new KthLargest(k, nums);
 * int param_1 = obj.add(val);
 */
```
