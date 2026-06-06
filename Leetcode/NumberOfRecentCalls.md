## 933. Number of Recent Calls

**Difficulty:** Easy

### Problem

You have a `RecentCounter` class which counts the number of recent requests within a certain time frame.

Implement the `RecentCounter` class:

- `RecentCounter()` Initializes the counter with zero recent requests.
- `int ping(int t)` Adds a new request at time `t`, where `t` represents some time in milliseconds, and returns the number of requests that has happened in the past 3000 milliseconds (including the new request). Specifically, return the number of requests that have happened in the inclusive range `[t - 3000, t]`.

It is guaranteed that every call to `ping` uses a strictly larger value of `t` than the previous call.

### Approach

Store all timestamps in a fixed-size array. On each `ping(t)`, append `t` and use binary search to find the first timestamp >= `t - 3000`. The count of valid requests is `currIndex - firstIndex`.

- **Time Complexity:** O(log N) per ping due to binary search.
- **Space Complexity:** O(1) — fixed array of size 10010.

---

## Code (Java)

```java
class RecentCounter {

    private int[] time = new int[10010];
    private int currIndex;

    public RecentCounter() {
        currIndex = 0;
    }

    public int ping(int t) {
        time[currIndex++] = t;
        int firstIndex = binarySearch(t-3000);
        return currIndex - firstIndex;
    }

    private int binarySearch(int t){
        int left = 0;
        int right = currIndex;

        while(left < right){
            int mid = (left+right)/2;

            if(time[mid] < t){
                left = mid+1;
            }
            else{
                right = mid;
            }
        }
        return left;
    }
}

/**
 * Your RecentCounter object will be instantiated and called as such:
 * RecentCounter obj = new RecentCounter();
 * int param_1 = obj.ping(t);
 */
```
