## 706. Design HashMap

**Difficulty:** Easy

### Problem

Design a HashMap without using any built-in hash table libraries.

Implement the `MyHashMap` class:

- `MyHashMap()` initializes the object with an empty map.
- `void put(int key, int value)` inserts a `(key, value)` pair into the HashMap. If the key already exists in the map, update the corresponding value.
- `int get(int key)` returns the value to which the specified key is mapped, or `-1` if this map contains no mapping for the key.
- `void remove(key)` removes the key and its corresponding value if the map contains the mapping for the key.

### Approach

Use an array of `LinkedList<Entry>` buckets (chaining) to handle collisions. The hash function maps each key to a bucket index using `key % SIZE`. For each operation, compute the bucket index, then traverse the linked list at that index to find, insert, update, or remove the entry.

- **Time Complexity:** O(N/K) average for all operations, where N is the number of keys and K is the number of buckets.
- **Space Complexity:** O(K + N)

---

## Code (Java)

```java
class MyHashMap {

    private static final int SIZE = 1000;
    private LinkedList<Entry>[] buckets;

    private static class Entry {
        int key;
        int value;

        Entry(int key, int value) {
            this.key = key;
            this.value = value;
        }
    }

    public MyHashMap() {
        buckets = new LinkedList[SIZE];
    }

    private int hash(int key) {
        return key % SIZE;
    }

    public void put(int key, int value) {
        int index = hash(key);

        if (buckets[index] == null) {
            buckets[index] = new LinkedList<>();
        }

        for (Entry entry : buckets[index]) {
            if (entry.key == key) {
                entry.value = value; // update
                return;
            }
        }

        buckets[index].add(new Entry(key, value));
    }

    public int get(int key) {
        int index = hash(key);

        if (buckets[index] == null) {
            return -1;
        }

        for (Entry entry : buckets[index]) {
            if (entry.key == key) {
                return entry.value;
            }
        }

        return -1;
    }

    public void remove(int key) {
        int index = hash(key);

        if (buckets[index] == null) {
            return;
        }

        Iterator<Entry> it = buckets[index].iterator();
        while (it.hasNext()) {
            if (it.next().key == key) {
                it.remove();
                return;
            }
        }
    }
}

/**
 * Your MyHashMap object will be instantiated and called as such:
 * MyHashMap obj = new MyHashMap();
 * obj.put(key,value);
 * int param_2 = obj.get(key);
 * obj.remove(key);
 */
```
