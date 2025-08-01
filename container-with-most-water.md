---
layout: default
title: "11. Container With Most Water"
permalink: /greedy/container-with-most-water
---

# 11. Container With Most Water

Difficulty: **Medium**

[Link to the problem in Leetcode](https://leetcode.com/problems/container-with-most-water/description/?envType=problem-list-v2&envId=greedy)

## Problem Statement as is from Leetcode 
You are given an integer array height of length `n`. There are `n` vertical lines drawn such that the two endpoints of the `i`-th line are `(i, 0)` and (`i`, `height[i]`).

Find two lines that together with the x-axis form a container, such that the container contains the most water.

Return the maximum amount of water a container can store.

Notice that you may not slant the container.

![Question Photo](https://sortira.github.io/intergrind/container-with-most-water-fig1.jpg "Example 1 Visualized")

Input: height = [1,8,6,2,5,4,8,3,7]

Output: 49

Explanation: The above vertical lines are represented by array [1,8,6,2,5,4,8,3,7]. In this case, the 
max area of water (blue section) the container can contain is 49.

## Explanation

To solve this, we shall use the greedy paradigm implemented using two-pointer approach. Let us assume `left` and `right` to be 2 pointers, with left pointing to the height of vertical line at the left index and similar for right. We shall iterate until `left` is on the left of `right` and calculate the volume as the product of the minimum of the two heights pointed at by the pointers times the horizontal difference between them (right - left). Then we shall increment left if the left-height is smaller than the right or decrement right if the right-height is smaller.

The greedy part of the solution is that at every step while calculating the area, we consider the smaller of the two vertical heights to be the bottleneck and hence remove it by progressing the pointer corresponding to the smaller height. Let's say the `height[left]` is smaller so we know that on the left side of `left` (i.e. any position obtained by decrementing `left`) has been visited before and hence not likely to yield a greater area so we move `left` forward sacrificing an unit of width in search of a better height. Even though we do not bruteforce, this solution explores the best possible combinations for every width.

## Code

### C++ Solution

```cpp
class Solution {
public:
    int maxArea(vector<int>& height) {
        int left = 0, right = height.size() - 1, maxvol = 0;
        while (left < right) {
            int currvol = min(height[left], height[right]) * (right - left);
            maxvol = max(maxvol, currvol);
            if (height[left] < height[right]) {
                left++;
            } else {
                right--;
            }
        }
        return maxvol;
    }
};
```
### Python Solution 

```python
class Solution(object):
    def maxArea(self, height):
        size = len(height)
        left = 0
        maxvol = -1
        right = size - 1
        while left <= right:
            currvol = min(height[left], height[right]) * (right - left)
            if currvol > maxvol:
                maxvol = currvol
            if height[left] <= height[right]:
                left = left + 1
            else:
                right = right - 1
        return maxvol
```

## Tags

Greedy, Two Pointers