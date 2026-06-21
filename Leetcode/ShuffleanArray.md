# Shuffle an Array

## Problem Description

Given an integer array `nums`, design an algorithm to randomly shuffle the array. All permutations of the array should be equally likely as a result of the shuffling.

Implement the `Solution` class:

- `Solution(int[] nums)` Initializes the object with the integer array `nums`.
- `int[] reset()` Resets the array to its original configuration and returns it.
- `int[] shuffle()` Returns a random shuffling of the array.

## Approach — Fisher-Yates Shuffle

For each index `i`, pick a random index from `[i, n-1]` and swap. This guarantees a uniform distribution across all `n!` permutations in O(n) time.

- Store a copy of the original array at construction time so `reset()` can restore it.
- `shuffle()` operates on `nums` in-place using the Fisher-Yates algorithm.

**Time Complexity:** O(n) for shuffle, O(n) for reset  
**Space Complexity:** O(n) for the original copy

## Solution

```java
class Solution {
    private int[] nums;
    private int[] original;
    private Random rand;

    public Solution(int[] nums) {
        this.nums = nums;
        this.original = Arrays.copyOf(nums, nums.length);
        this.rand = new Random();
    }
    
    public int[] reset() {
        nums = Arrays.copyOf(original, original.length);
        return nums;
    }
    
    public int[] shuffle() {
        for(int i=0; i<nums.length; i++){
            int randomIndex = i + rand.nextInt(nums.length-i);
            swap(i, randomIndex);
        }
        return nums;
    }

    private void swap(int i, int j){
        int temp = nums[i];
        nums[i] = nums[j];
        nums[j] = temp;
    }
}

/**
 * Your Solution object will be instantiated and called as such:
 * Solution obj = new Solution(nums);
 * int[] param_1 = obj.reset();
 * int[] param_2 = obj.shuffle();
 */
```
