# Coding Problems

A curated collection of coding interview problems and reference solutions focused on the patterns that show up most often in software engineering interviews.

This repository is best used as a **pattern-first interview prep bank**. Instead of memorizing isolated problems, use each solution to learn the underlying algorithm, data structure, and decision-making process.

---

## What this repository covers

The problems in this repo mainly fall into these interview categories:

* Arrays and Hashing
* Two Pointers
* Sliding Window
* Prefix Sum
* Binary Search
* Linked Lists
* Trees and Binary Search Trees
* Graphs
* Dynamic Programming
* Backtracking
* Intervals
* Design Problems
* Parsing and String Manipulation

You will find classic problems such as:

* Two Sum
* 3Sum
* Product of Array Except Self
* Longest Substring Without Repeating Characters
* Minimum Window Substring
* Merge Intervals
* Coin Change
* Number of Islands
* Course Schedule
* Lowest Common Ancestor
* Serialize and Deserialize Binary Tree
* LRU Cache
* Time-Based Key Value Store

---

## How to use this repo

### 1. Study by pattern, not by filename

When opening a problem, first ask:

* What is the pattern?
* What data structure is doing the heavy lifting?
* What is the target time complexity?
* What edge cases matter?

### 2. Learn the reusable templates

A large number of interview questions reduce to a small set of templates:

* HashMap lookup
* Two pointers on sorted data
* Sliding window
* Prefix sum + frequency map
* DFS / BFS
* Tree recursion
* Binary search on boundary
* Backtracking
* Dynamic programming state transitions
* Design with HashMap + helper structure

### 3. Re-solve problems without looking

A good workflow is:

1. Read the problem
2. Identify the pattern
3. State time and space complexity
4. Code the solution from memory
5. Compare with the reference implementation
6. Revisit it later until the pattern becomes automatic

---

## Interview-ready pattern guide

### Arrays and Hashing

Use for complement lookup, frequency counting, deduplication, and fast membership checks.

Common tools:

* `HashMap`
* `HashSet`
* prefix arrays

Representative problems:

* `TwoSum`
* `LongestConsecutiveSequence`
* `IntersectionofTwoArrays`
* `InsertDeleteGetRandom`

### Two Pointers

Best for sorted arrays, palindrome checks, in-place filtering, and interval-style scans.

Representative problems:

* `TwoSumII`
* `ValidPalindrome`
* `MergeSortedArray`
* `RemoveDuplicatesfromSortedArray`
* `TrappingRainWater2Pointer`

### Sliding Window

Use when the question asks for a longest, shortest, or count-based condition over a contiguous range.

Representative problems:

* `LongestSubstringWithoutRepeatingCharacters`
* `FindAllAnagrams`
* `PermutationsInString`
* `MinWindowSubstring`
* `LongestSubStringKDistinctCharacterss`

### Prefix Sum

Use when subarray sums, divisible conditions, or repeated range queries appear.

Representative problems:

* `SubarraySumEqualsK`
* `ContinuousSubArraySum`
* `RangeSumQuery2D.md`

### Binary Search

Use for sorted arrays, boundary search, monotonic conditions, and indexed lookup over ordered data.

Representative problems:

* `FirstBadVersion`
* `FindPeakElement`
* `FirstLastinSortedArray`
* `RandomPickWithWeight`
* `TimeBasedKey-ValueStore`

### Trees

Use DFS for path-based or structural problems, and BFS for level-based traversal.

Representative problems:

* `ValidBinarySearchTree`
* `LowestCommonAncestorBinaryTree`
* `DiameterOfTree`
* `MaximumPathSum`
* `SerializeDeserializeBinaryTree`
* `BinaryTreeLevelOrderTraversal.md`

### Graphs

Think in terms of traversal, connected components, cycle detection, and topological ordering.

Representative problems:

* `NumberOfIsland`
* `CourseSchedule`
* `ClonGraph`

### Dynamic Programming

Use when the brute-force version repeats the same subproblems.

Representative problems:

* `ClimbingStairs`
* `CoinChange`
* `DecodeWays`
* `BestBuyandSellStockIII`

### Backtracking

Use for combinations, permutations, placements, expression generation, and partitioning problems.

Representative problems:

* `GenerateParentheses`
* `NQueens`
* `Permutation`
* `PalindromePartitioning`
* `ExpressionAddOperator`

### Design Problems

These usually combine a `HashMap` with a helper structure that supports the needed operations efficiently.

Representative problems:

* `LRUCache`
* `InsertDeleteGetRandom`
* `MovingAverageDataStream`
* `StockPriceFluctuation`
* `TimeBasedKey-ValueStore`

---

## Core data structures to remember

These show up repeatedly across the repository and in interviews:

* `HashMap`
* `HashSet`
* `ArrayList`
* `Stack`
* `Queue`
* `Deque`
* `PriorityQueue`
* `LinkedList`
* `TreeMap`
* `TreeSet`
* binary tree nodes
* graph adjacency lists
* doubly linked list

High-value combinations:

* `HashMap + Doubly Linked List` → LRU Cache
* `HashMap + ArrayList` → randomized set design
* `Prefix Sum + HashMap` → subarray counting
* `Deque` → sliding window maximum
* `TreeMap + HashMap` → ordered updates with fast lookup
* `List + Binary Search` → time-based retrieval

---

## Problems worth mastering first

If you are using this repo for interviews, start with these:

1. `TwoSum`
2. `3Sum-done`
3. `LongestSubstringWithoutRepeatingCharacters`
4. `MinWindowSubstring`
5. `SubarraySumEqualsK`
6. `MergeIntervals`
7. `CoinChange`
8. `NumberOfIsland`
9. `CourseSchedule`
10. `ValidBinarySearchTree`
11. `LowestCommonAncestorBinaryTree`
12. `SerializeDeserializeBinaryTree`
13. `NQueens`
14. `LRUCache`
15. `TimeBasedKey-ValueStore`

These cover most of the reusable patterns that appear again and again.

---

## Suggested study plan

### Phase 1: Foundations

* Arrays and Hashing
* Two Pointers
* Sliding Window
* Prefix Sum

### Phase 2: Core Traversals

* Linked Lists
* Trees
* Graphs
* Binary Search

### Phase 3: Advanced Problem Solving

* Dynamic Programming
* Backtracking
* Intervals
* Design Problems

### Phase 4: Review

* Re-solve the most important problems without help
* Focus on explaining the pattern before coding
* Practice time and space complexity discussion aloud

---

## Quick Cheat Sheet

### Problem clue → pattern

| Clue                                         | Pattern              |
| -------------------------------------------- | -------------------- |
| pair, target, complement                     | HashMap              |
| sorted array, pair/triplet                   | Two pointers         |
| longest/shortest substring                   | Sliding window       |
| subarray sum / count / divisible by k        | Prefix Sum + HashMap |
| overlapping ranges                           | Sort + Merge         |
| kth / top k                                  | Heap or Quickselect  |
| first / last / boundary / peak               | Binary Search        |
| min steps / count ways / best score          | Dynamic Programming  |
| all combinations / permutations / placements | Backtracking         |
| islands / components / prerequisites         | DFS / BFS / Graph    |
| tree levels                                  | BFS                  |
| tree path / diameter / BST / LCA             | DFS                  |
| cache / random / timestamps                  | Design               |

### Core data structures

* HashMap
* HashSet
* Array / ArrayList
* Stack
* Queue / Deque
* PriorityQueue
* LinkedList
* TreeMap / TreeSet
* Binary Tree
* Graph adjacency list

### High-value combinations

* HashMap + Doubly Linked List → LRU Cache
* HashMap + ArrayList → Insert Delete GetRandom
* Prefix Sum + HashMap → Subarray Sum Equals K
* Deque → Sliding Window Maximum
* TreeMap + HashMap → ordered update problems
* List + Binary Search → Time-Based Key Value Store

### Mini templates

#### HashMap complement

```java
Map<Integer, Integer> map = new HashMap<>();
for (int i = 0; i < nums.length; i++) {
    int need = target - nums[i];
    if (map.containsKey(need)) return new int[]{map.get(need), i};
    map.put(nums[i], i);
}
```

#### Sliding window

```java
int left = 0;
for (int right = 0; right < s.length(); right++) {
    // include right
    while (windowInvalid) {
        // exclude left
        left++;
    }
    // update answer
}
```

#### Prefix sum + frequency map

```java
Map<Integer, Integer> freq = new HashMap<>();
freq.put(0, 1);
int sum = 0, ans = 0;
for (int x : nums) {
    sum += x;
    ans += freq.getOrDefault(sum - k, 0);
    freq.put(sum, freq.getOrDefault(sum, 0) + 1);
}
```

#### Binary search

```java
int lo = 0, hi = n - 1;
while (lo < hi) {
    int mid = lo + (hi - lo) / 2;
    if (condition(mid)) hi = mid;
    else lo = mid + 1;
}
return lo;
```

#### Tree DFS

```java
int dfs(TreeNode node) {
    if (node == null) return 0;
    int left = dfs(node.left);
    int right = dfs(node.right);
    return ...;
}
```

#### Backtracking

```java
void backtrack(...) {
    if (baseCase) {
        result.add(...);
        return;
    }
    for (...) {
        // choose
        backtrack(...);
        // unchoose
    }
}
```

### 30-second interview checklist

* Name the pattern before coding
* State time and space complexity
* List edge cases
* Code the clean version first
* Trace one example manually

## Interview checklist

Before you code, make sure you can answer:

* What pattern does this problem match?
* Why is this better than brute force?
* What are the time and space complexities?
* What edge cases do I need to handle?
* Can I explain the solution clearly in a few sentences?

---

## Goal of this repo

The goal is not just to collect solutions.

The goal is to build strong pattern recognition so that when a new interview question appears, you can quickly map it to a known approach and solve it with confidence.

---

## License

Add a license section here if you want to make the repository publicly reusable under a specific license.

