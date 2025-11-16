# Maximum Subarray Sum using Kadane's Algorithm

## Problem Description
Given an array of integers, find the contiguous subarray within it that has the largest possible sum. The goal is to return this maximum sum.

## Intuition Summary
Kadane's algorithm solves the maximum subarray sum problem using a dynamic programming approach. The core idea is to iterate through the array, maintaining two variables: `current_max` and `global_max`. `current_max` tracks the maximum sum of a subarray ending at the current position. For each element, `current_max` is updated by choosing the maximum between the current element itself (starting a new subarray) and the current element added to the previous `current_max` (extending the current subarray). If `current_max` ever becomes negative, it's effectively reset to the current element, as a negative prefix will only diminish future sums. `global_max` stores the overall maximum sum found across all subarrays encountered so far, and it's updated whenever `current_max` exceeds it. This process ensures that the largest possible contiguous subarray sum is captured efficiently, even when dealing with negative numbers.

## Time Complexity
O(N) because the algorithm iterates through the array of N elements exactly once to compute the maximum subarray sum. Each element is processed in constant time.

## Space Complexity
O(1) auxiliary space because the algorithm only uses a few constant-space variables (`current_max`, `global_max`, and loop index) regardless of the input array size.

## Key Learnings
*   Kadane's algorithm is a classic and efficient dynamic programming solution for the maximum subarray sum problem.
*   The core idea involves keeping track of the maximum sum ending at the current position and the overall maximum sum found.
*   A key optimization is resetting the 'current_max' subarray sum when it becomes negative, as it's better to start a new subarray from the next element.
*   The algorithm handles arrays with all positive, all negative, and mixed positive/negative numbers gracefully.
*   It demonstrates the power of greedy choices within a dynamic programming framework, where locally optimal decisions lead to a globally optimal solution.
*   Understanding edge cases like single-element arrays or arrays containing zeroes is crucial for a robust implementation.
*   The solution is iterative and highly space-efficient, requiring only a constant amount of auxiliary space.

## Similar Problems
*   Maximum Product Subarray
*   Longest Increasing Subsequence
*   Minimum Subarray Sum
*   Subarray Sum Equals K
