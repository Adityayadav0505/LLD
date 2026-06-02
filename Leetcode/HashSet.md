# Day 01 — Design a HashSet

**Date:** 2026-06-03  
**Difficulty:** Easy  
**Topic:** Hashing, Data Structures

---

## Problem

Design a HashSet without using any built-in hash table libraries.

Implement the `MyHashSet` class:

- `void add(key)` — Inserts the value `key` into the HashSet.
- `bool contains(key)` — Returns whether the value `key` exists in the HashSet or not.
- `void remove(key)` — Removes the value `key` from the HashSet. If `key` does not exist, do nothing.

---

## Approach

- Use an array of `LinkedList<Integer>` buckets of fixed size (1000).
- Map each key to a bucket via `key % SIZE` (hash function).
- Each bucket holds a linked list to handle **collisions via chaining**.
- On `add`: initialize the bucket if null, then insert only if not already present.
- On `remove`: cast to `Integer` to call `remove(Object)` (not `remove(index)`).
- On `contains`: check if bucket is non-null and contains the key.

**Time Complexity:** O(n/k) average per operation, where n = number of keys, k = bucket count  
**Space Complexity:** O(n + k)

---

## Code (Java)

```java
class MyHashSet {
    private static final int SIZE = 1000;
    private LinkedList<Integer>[] buckets;

    public MyHashSet() {
        buckets = new LinkedList[SIZE];
    }

    private int hash(int key) {
        return key % SIZE;
    }

    public void add(int key) {
        int index = hash(key);
        if (buckets[index] == null) {
            buckets[index] = new LinkedList<>();
        }
        if (!buckets[index].contains(key))
            buckets[index].add(key);
    }

    public void remove(int key) {
        int index = hash(key);
        if (buckets[index] != null) {
            buckets[index].remove((Integer) key);
        }
    }

    public boolean contains(int key) {
        int index = hash(key);
        return buckets[index] != null && buckets[index].contains(key);
    }
}

/**
 * Your MyHashSet object will be instantiated and called as such:
 * MyHashSet obj = new MyHashSet();
 * obj.add(key);
 * obj.remove(key);
 * boolean param_3 = obj.contains(key);
 */
```
