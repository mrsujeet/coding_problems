/*
https://leetcode.com/problems/next-permutation/description/

A permutation of an array of integers is an arrangement of its members into a sequence or linear order.

For example, for arr = [1,2,3], the following are all the permutations of arr: [1,2,3], [1,3,2], [2, 1, 3], [2, 3, 1], [3,1,2], [3,2,1].
The next permutation of an array of integers is the next lexicographically greater permutation of its integer. More formally, if all the permutations of the array are sorted in one container according to their lexicographical order, then the next permutation of that array is the permutation that follows it in the sorted container. If such arrangement is not possible, the array must be rearranged as the lowest possible order (i.e., sorted in ascending order).

For example, the next permutation of arr = [1,2,3] is [1,3,2].
Similarly, the next permutation of arr = [2,3,1] is [3,1,2].
While the next permutation of arr = [3,2,1] is [1,2,3] because [3,2,1] does not have a lexicographical larger rearrangement.
Given an array of integers nums, find the next permutation of nums.

The replacement must be in place and use only constant extra memory.

 

Example 1:

Input: nums = [1,2,3]
Output: [1,3,2]
Example 2:

Input: nums = [3,2,1]
Output: [1,2,3]
Example 3:

Input: nums = [1,1,5]
Output: [1,5,1]
 



*/

class Solution {
    public void nextPermutation(int[] nums) {
        int n = nums.length;

        // 1) Find the first index i from the right where nums[i] < nums[i+1]
        int i = n - 2;
        while (i >= 0 && nums[i] >= nums[i + 1]) i--;

        if (i >= 0) {
            // 2) Find the first index j from the right where nums[j] > nums[i]
            int j = n - 1;
            while (nums[j] <= nums[i]) j--;
            swap(nums, i, j);
        }

        // 3) Reverse the suffix starting at i+1 to make it increasing (smallest)
        reverse(nums, i + 1, n - 1);
    }

    private void swap(int[] a, int i, int j) {
        int t = a[i]; a[i] = a[j]; a[j] = t;
    }

    private void reverse(int[] a, int l, int r) {
        while (l < r) swap(a, l++, r--);
    }
}

/*

## Example:

`nums = [1, 4, 7, 6, 5, 3, 2]`

We want the **next lexicographic permutation**.

---

### 🔹 Step 1: Find pivot `i`

Scan from the right until you find the first `nums[i] < nums[i+1]`.

* Compare `3 < 2` ❌
* Compare `5 < 3` ❌
* Compare `6 < 5` ❌
* Compare `7 < 6` ❌
* Compare `4 < 7` ✅

So, `i = 1` (`nums[i] = 4`).

This means everything from index 2 onward `[7,6,5,3,2]` is a **non-increasing suffix**.
So when we scan from right to left, we are looking for the longest tail part of the array that is sorted in descending order.

---

### 🔹 Step 2: Find `j`

Find the rightmost element **greater than `nums[i] = 4`**.

From the right:

* `2 > 4` ❌
* `3 > 4` ❌
* `5 > 4` ✅ → stop at `j = 4`.

So, `nums[j] = 5`.

---

### 🔹 Step 3: Swap `i` and `j`

Swap `nums[i]` (4) with `nums[j]` (5):

Before swap: `[1, 4, 7, 6, 5, 3, 2]`
After swap:  `[1, 5, 7, 6, 4, 3, 2]`

---

### 🔹 Step 4: Reverse suffix (from `i+1 = 2` to end)

Suffix is `[7, 6, 4, 3, 2]`.
Reverse → `[2, 3, 4, 6, 7]`.

Final result:
`[1, 5, 2, 3, 4, 6, 7]`

---

✅ This is the **next permutation** after `[1,4,7,6,5,3,2]`.

---

### Why it works here

* `[1,4,...]` was the prefix. We bumped `4` → `5` (the next higher choice).
* Then we reset the suffix to smallest possible `[2,3,4,6,7]`.
* That makes the result *just one step ahead* in lexicographic order.

*/
