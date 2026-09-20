# Leetcode_Day50
# Day 50 — Find the Duplicate Number

## 🧩 Problem

**LeetCode 287 — Find the Duplicate Number**

Given an array `nums` containing `n + 1` integers where each integer is in the range `[1, n]`, exactly one number is repeated.

The goal is to find the repeated number **without modifying the array** and using only **constant extra space**.

---

## 💡 Approach

I solved this problem using **Floyd's Cycle Detection Algorithm** (Tortoise and Hare).

The main idea is to treat the array like a linked list:

- Each value points to the next index.
- Because one number is repeated, a cycle is guaranteed to exist.
- We use two pointers:
  - `slow` moves one step at a time.
  - `fast` moves two steps at a time.
- When they meet, a cycle exists.
- Then we reset another pointer to the beginning and move both pointers one step at a time.
- The point where they meet again is the duplicate number.

### Steps

1. Initialize `slow` and `fast` with `nums[0]`.
2. Move:
   - `slow = nums[slow]`
   - `fast = nums[nums[fast]]`
3. Continue until `slow == fast`.
4. Initialize another pointer `slow2 = nums[0]`.
5. Move both pointers one step at a time:
   - `slow = nums[slow]`
   - `slow2 = nums[slow2]`
6. When they meet, return `slow`.

---

## 💻 Java Solution

```java
class Solution {
    public int findDuplicate(int[] nums) {
        int slow = nums[0];
        int fast = nums[0];

        do {
            slow = nums[slow];
            fast = nums[nums[fast]];
        } while (slow != fast);

        int slow2 = nums[0];

        while (slow != slow2) {
            slow = nums[slow];
            slow2 = nums[slow2];
        }

        return slow;
    }
}
⏱️ Complexity
Time Complexity: O(n)
Space Complexity: O(1)
📚 What I Learned

Today I learned how an array can be viewed in a completely different way.

Instead of treating the elements only as numbers, I learned to treat each value as a pointer to another position. This transforms the problem into a cycle detection problem.

The most important concept I learned was Floyd's Cycle Detection Algorithm, which can find a cycle without using extra memory.

🎯 Takeaway

Sometimes the solution is not about changing the data.

It is about changing the way we look at the data.
