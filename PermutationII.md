/*

https://leetcode.com/problems/permutations-ii/description/

Given a collection of numbers, nums, that might contain duplicates, return all possible unique permutations in any order.

 

Example 1:

Input: nums = [1,1,2]
Output:
[[1,1,2],
 [1,2,1],
 [2,1,1]]
Example 2:

Input: nums = [1,2,3]
Output: [[1,2,3],[1,3,2],[2,1,3],[2,3,1],[3,1,2],[3,2,1]]
 

Constraints:

1 <= nums.length <= 8
-10 <= nums[i] <= 10


*/

import java.util.*;

public class PermuteUniqueWithComments {

    /**
     * Returns all unique permutations of nums (which may contain duplicates).
     *
     * Key ideas:
     * 1) Sort first: groups duplicates together so we can enforce a canonical pick order.
     * 2) Backtracking with:
     *    - used[i]       -> prevents reusing the same INDEX twice on the same recursion path.
     *    - duplicate rule -> at the SAME DEPTH (same slot), don't take later duplicate before the earlier one.
     */
    public static List<List<Integer>> permuteUnique(int[] nums) {
        Arrays.sort(nums); // Sorting lets us detect duplicates as neighbors.
        List<List<Integer>> ans = new ArrayList<>();
        boolean[] used = new boolean[nums.length]; // used[i] == true means index i is already in current path
        backtrack(nums, used, new ArrayList<>(), ans);
        return ans;
    }

    /**
     * @param nums the sorted input
     * @param used tracks which INDICES are already in the current partial permutation (path)
     * @param path the current partial permutation
     * @param ans  all collected unique permutations
     *
     * "Depth" explanation:
     * - Each recursive call represents a specific "depth" = how many numbers are already in 'path'.
     * - Depth 0 -> choose the 1st slot, Depth 1 -> choose the 2nd slot, etc.
     * - Inside ONE call (one depth/slot), the for-loop's iterations are "sibling choices".
     *   The duplicate-skip rule acts among these siblings at this SAME depth.
     */
    private static void backtrack(int[] nums, boolean[] used, List<Integer> path, List<List<Integer>> ans) {
        // Base case: we filled all slots -> record a permutation.
        if (path.size() == nums.length) {
            // IMPORTANT: snapshot the current path. 'path' is reused & mutated by backtracking,
            // so we must copy it now; otherwise all entries in ans would point to the same list.
            ans.add(new ArrayList<>(path));
            return;
        }

        // Try each index as the next element to place in THIS slot (THIS recursion depth)
        for (int i = 0; i < nums.length; i++) {

            // 1) Don't reuse the same index twice on the SAME recursion path.
            //    This is index-based (not value-based). You *can* use another equal value
            //    from a different index, provided that index isn't used yet.
            if (used[i]) continue;

            // 2) Duplicate-skip rule (the de-dup heart):
            //    If nums[i] == nums[i-1] and the previous equal element (i-1) was NOT used
            //    in THIS slot/THIS depth yet, then skip nums[i].
            //
            //    Meaning: Among equal numbers at the SAME depth, you must pick them in left-to-right order.
            //    This avoids generating two sibling branches that differ only by which duplicate you picked first.
            //
            //    "Same depth" = inside this very call frame (this slot), while this for-loop runs.
            //    This rule does NOT block using the duplicate at a deeper depth (next slot).
            //
            //    Example for [1,1,2]:
            //      - At depth 0 (choosing slot 0), we allow i=0 (first 1), and skip i=1 (second 1) *at this depth*,
            //        because used[0] is false at this depth.
            //      - After we pick i=0 and go deeper to depth 1, used[0] is true, so i=1 becomes allowed there.
            //        That's how we still form [1,1,2] (112).
            if (i > 0 && nums[i] == nums[i - 1] && !used[i - 1]) {
                continue;
            }

            // Choose nums[i] for this slot
            used[i] = true;
            path.add(nums[i]);

            // Recurse to the next slot (deeper depth)
            backtrack(nums, used, path, ans);

            // Undo the choice (backtrack) so we can try other indices for this slot
            path.remove(path.size() - 1);
            used[i] = false;
        }
    }

    // --- Optional demo driver ---
    public static void main(String[] args) {
        int[] a = {1, 1, 2};
        List<List<Integer>> res = permuteUnique(a);
        System.out.println(res); // Expected: [[1,1,2], [1,2,1], [2,1,1]]
    }
}

/*
FAQ (quick recap):

Q1) "path is already an ArrayList; why new ArrayList<>(path)?"
A1) Backtracking mutates the same 'path' list (add/remove). If you add 'path' directly,
    every entry in 'ans' would reference the same list object, which keeps changing.
    'new ArrayList<>(path)' takes a snapshot at that moment.

Q2) What does 'used[i]' guard?
A2) It prevents reusing the same array INDEX twice in one permutation (same recursion path).
    It's index-based, not value-based.

Q3) What does the duplicate-skip condition do?
    (i > 0 && nums[i] == nums[i-1] && !used[i-1])
A3) At the SAME depth (same slot), among equal numbers, only choose the leftmost unused one.
    This kills duplicate sibling branches. It does NOT stop you from using the second duplicate
    at a deeper depth (where used[i-1] may be true), which is how [1,1,2] still appears.

Q4) What is "same depth"?
A4) The current recursion level = which slot you’re filling now. The for-loop’s options inside a single call
    are siblings at the same depth.

Time complexity: O(k) to output k unique permutations (bounded by n! in the all-distinct case).
Extra space: O(n) for recursion + used[] (not counting output).
*/
