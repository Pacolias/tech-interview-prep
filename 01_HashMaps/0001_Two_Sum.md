# 1. Two Sum

- **Link:** [LeetCode - Two Sum](https://leetcode.com/problems/two-sum/)
- **Difficulty:** Easy
- **Algorithmic Pattern:** Hash Map (One-Pass)

## 💡 The "Aha! Moment" (Intuition)
Instead of using two nested loops to look ahead (brute force $O(n^2)$), we use a `HashMap` to "remember the past". 
As we iterate through the array, we calculate what number we are missing (`target - currentNumber`). If that number is already in our map, we have found the pair. If not, we store the current number and its index in the map and keep moving forward.

## ⏱️ Complexity
- **Time:** $O(n)$ -> We traverse the array exactly once. HashMap lookups take $O(1)$ amortized time.
- **Space:** $O(n)$ -> In the worst-case scenario, we store all the array elements in the HashMap.

## 💻 Code (Java)

```java
class Solution {
    public int[] twoSum(int[] nums, int target) {
        HashMap<Integer, Integer> auxMap = new HashMap<>();

        for(int i = 0; i < nums.length; i++){
            int currentNumber = nums[i];
            int whatsMissing = target - nums[i];

            if(auxMap.containsKey(whatsMissing)) {
                return new int[]{auxMap.get(whatsMissing), i}; 
            }

            auxMap.put(currentNumber, i);
        }

        return new int[]{};
    }
}
