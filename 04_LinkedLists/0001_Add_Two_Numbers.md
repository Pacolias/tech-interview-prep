# 2. Add Two Numbers

- **Link:** [LeetCode - Add Two Numbers](https://leetcode.com/problems/add-two-numbers/)
- **Difficulty:** Medium
- **Algorithmic Pattern:** Linked List, Recursion, Math

## 💡 The "Aha! Moment" (Intuition)
Instead of relying on nested `if/else` statements to handle different list lengths and carries, we can abstract the process using pure math and recursion. 
By safely extracting the node values using ternary operators (`(l1 == null) ? 0 : l1.val`), we treat `null` nodes as `0`. We then apply elementary addition: `sum % 10` gives us the current digit, and `sum / 10` gives us the carry for the next recursive call. 
The recursion elegantly terminates (Base Case) only when both nodes are exhausted AND there is no carry left.

*Note on Trade-offs:* While this recursive approach is highly readable and declarative, it uses $O(\max(m, n))$ auxiliary space on the Call Stack. For massive datasets, an iterative approach with a `dummyHead` would be preferred to achieve $O(1)$ auxiliary space.

## ⏱️ Complexity
- **Time:** $O(\max(m, n))$ -> We traverse both lists completely, where $m$ and $n$ are the lengths of `l1` and `l2`.
- **Space:** $O(\max(m, n))$ -> The recursion depth goes as deep as the longest list (plus one extra frame if there's a final carry), consuming stack memory.

## 💻 Code (Java)

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 * int val;
 * ListNode next;
 * ListNode() {}
 * ListNode(int val) { this.val = val; }
 * ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */
class Solution {
    public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        return addTwoNumbersRecursive(l1, l2, 0);
    }

    private ListNode addTwoNumbersRecursive(ListNode l1, ListNode l2, int carry){

        if(l1 == null && l2 == null && carry == 0) // Base Case
            return null;

        int val1 = (l1 == null) ? 0 : l1.val;
        int val2 = (l2 == null) ? 0 : l2.val;
        int sum = val1 + val2 + carry;

        int val = sum % 10;
        carry = sum / 10;
        ListNode sol = new ListNode(val);

        ListNode next1 = (l1 == null) ? null : l1.next;
        ListNode next2 = (l2 == null) ? null : l2.next;

        sol.next = addTwoNumbersRecursive(next1, next2, carry);

        return sol;
    }
}
