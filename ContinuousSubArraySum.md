/*
https://leetcode.com/problems/continuous-subarray-sum/description/
https://leetcode.com/explore/interview/card/facebook/55/dynamic-programming-3/3038/

Given an integer array nums and an integer k, return true if nums has a good subarray or false otherwise.

A good subarray is a subarray where:

its length is at least two, and
the sum of the elements of the subarray is a multiple of k.
Note that:

A subarray is a contiguous part of the array.
An integer x is a multiple of k if there exists an integer n such that x = n * k. 0 is always a multiple of k.
 

Example 1:

Input: nums = [23,2,4,6,7], k = 6
Output: true
Explanation: [2, 4] is a continuous subarray of size 2 whose elements sum up to 6.


How it works ?

If prefixSum[i] % k == prefixSum[j] % k and i > j, then
(prefixSum[i] - prefixSum[j]) % k == 0, i.e., the subarray (j+1..i) sum is a multiple of k. We enforce i - j >= 2.

Time: O(n)
Space: O(min(n, |k|)) for the map of remainders (O(n) worst-case)

*/


import java.util.*;

class Solution {
    public boolean checkSubarraySum(int[] nums, int k) {
        Map<Integer, Integer> map = new HashMap<>();
        map.put(0, -1);  // Handle edge case: subarray starting at index 0

        int runningSum = 0;

        for (int i = 0; i < nums.length; i++) {
            runningSum += nums[i];
            int mod = k == 0 ? runningSum : runningSum % k;

            if (map.containsKey(mod)) {
                if (i - map.get(mod) > 1) {
                    return true;  // Found a valid subarray
                }
            } else {
                map.put(mod, i);  // Store only the first occurrence
            }
        }

        return false;
    }
}
/*

### 📌 What Does `map.put(0, -1)` Mean?

* We're storing that the **remainder `0`** (i.e., sum divisible by `k`) was seen at **index `-1`**.
* This is a **sentinel value** that allows us to detect a valid subarray starting from the very beginning.

---

### 🔍 Why `-1` and not `0`?

Suppose your `nums = [5, 1]` and `k = 6`.

* `runningSum = 6` at index `1`, so `runningSum % k = 0`
* We check if `map.containsKey(0)` → it is (from `map.put(0, -1)`)
* `i - map.get(0) = 1 - (-1) = 2` → this subarray has **length ≥ 2**

✅ So `[5, 1]` is a valid subarray.

Without `map.put(0, -1)`, we’d **miss** the fact that `[5, 1]` is divisible by `k = 6`.



* Ensures that subarrays starting from index 0 are checked.
* The `-1` is used because the "previous" index before the array starts is considered to be `-1`.
* Allows correct calculation of subarray length with `i - prevIndex`.


*/
