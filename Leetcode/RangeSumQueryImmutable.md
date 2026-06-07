## Description

Given an integer array `nums`, handle multiple queries of the following type:

Calculate the sum of the elements of `nums` between indices `left` and `right` inclusive where `left <= right`.

Implement the `NumArray` class:

- `NumArray(int[] nums)` Initializes the object with the integer array `nums`.
- `int sumRange(int left, int right)` Returns the sum of the elements of `nums` between indices `left` and `right` inclusive (i.e. `nums[left] + nums[left + 1] + ... + nums[right]`).

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
