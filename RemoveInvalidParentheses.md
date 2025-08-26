/*

https://leetcode.com/problems/remove-invalid-parentheses/

Given a string s that contains parentheses and letters, remove the minimum number of invalid parentheses to make the input string valid.

Return a list of unique strings that are valid with the minimum number of removals. You may return the answer in any order.

 

Example 1:

Input: s = "()())()"
Output: ["(())()","()()()"]
Example 2:

Input: s = "(a)())()"
Output: ["(a())()","(a)()()"]
Example 3:

Input: s = ")("
Output: [""]
 

Constraints:

1 <= s.length <= 25
s consists of lowercase English letters and parentheses '(' and ')'.
There will be at most 20 parentheses in s.


*/




import java.util.*;

public class Solution {
    public List<String> removeInvalidParentheses(String s) {
        List<String> result = new ArrayList<>();
        if (s == null) return result;

        Set<String> visited = new HashSet<>();     // Avoid reprocessing the same string
        Queue<String> queue = new LinkedList<>();  // BFS queue for level-by-level processing

        queue.offer(s);
        visited.add(s);
        boolean foundValidLevel = false;

        while (!queue.isEmpty()) {
            String curr = queue.poll();

            // ✅ If current string is valid, add to result
            if (isValid(curr)) {
                result.add(curr);
                foundValidLevel = true;
            }

            // ✅ Stop exploring deeper levels once we find valid strings
            if (foundValidLevel) continue;

            // Try removing one parenthesis at each index
            for (int i = 0; i < curr.length(); i++) {
                char ch = curr.charAt(i);

                // Only try removing '(' or ')'
                if (ch != '(' && ch != ')') continue;

                // Form a new string with the i-th character removed
                String next = curr.substring(0, i) + curr.substring(i + 1);

                // Add to queue if not seen before
                if (!visited.contains(next)) {
                    queue.offer(next);
                    visited.add(next);
                }
            }
        }

        return result;
    }

    // ✅ Helper method to check if string has balanced parentheses
    private boolean isValid(String s) {
        int balance = 0;

        for (char ch : s.toCharArray()) {
            if (ch == '(') {
                balance++;       // Open parenthesis found
            } else if (ch == ')') {
                if (balance == 0) return false;  // Too many closing
                balance--;       // Match closing with opening
            }
        }

        return balance == 0; // True if no unmatched '(' left
    }
}
/*



*/
