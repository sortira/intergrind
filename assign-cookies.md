---
layout: default
title: "455. Assign Cookies"
permalink: /greedy/assign-cookies
---

# 455. Assign Cookies

Difficulty: **Easy**

[Link to the problem in Leetcode](https://leetcode.com/problems/assign-cookies/?envType=problem-list-v2&envId=greedy)

## Problem Statement as is from Leetcode 

Assume you are an awesome parent and want to give your children some cookies. But, you should give each child at most one cookie.

Each child i has a greed factor g[i], which is the minimum size of a cookie that the child will be content with; and each cookie j has a size s[j]. If s[j] >= g[i], we can assign the cookie j to the child i, and the child i will be content. Your goal is to maximize the number of your content children and output the maximum number.

 

Example 1:

Input: g = [1,2,3], s = [1,1]

Output: 1

Explanation: You have 3 children and 2 cookies. The greed factors of 3 children are 1, 2, 3. 
And even though you have 2 cookies, since their size is both 1, you could only make the child whose greed factor is 1 content.

You need to output 1.

Example 2:

Input: g = [1,2], s = [1,2,3]

Output: 2

Explanation: You have 2 children and 3 cookies. The greed factors of 2 children are 1, 2. 
You have 3 cookies and their sizes are big enough to gratify all of the children, 

You need to output 2.
 

## Explanation

We shall use the greedy approach implemented using 2 pointers. First let us sort the two arrays `s` and `g`. Then we shall set the two pointers one each to the last index of both arrays. Our approach here is to try giving the largest cookie to the greediest child, and if the greed of the greediest child is larger than the size of the largest cookie, then we decrement the child pointer to progress down the `g` array to find a child whose greed satisfies the current cookie size condition. Once such a match is found, we increment answer and then continue the process till we reach the ends of both the arrays. 

## Code

```cpp
class Solution {
public:
    int findContentChildren(vector<int>& g, vector<int>& s) {
        sort(g.begin(), g.end());
        sort(s.begin(), s.end());
        int childPtr = g.size() - 1, cookiePtr = s.size() - 1, answer = 0;
        while (childPtr >= 0 && cookiePtr >= 0) {
            if (g[childPtr] > s[cookiePtr])
                childPtr--;
            else {
                childPtr--;
                cookiePtr--;
                answer++;
            }
        }
        return answer;
    }
};
```

## Tags

Greedy, Two Pointers