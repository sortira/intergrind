---
layout: default
title: "409. Longest Palindrome"
permalink: /greedy/longest-palindrome
---

# 409. Longest Palindrome

Difficulty: **Easy**

[Link to the problem in Leetcode](https://leetcode.com/problems/longest-palindrome/description/?envType=problem-list-v2&envId=greedy)

## Problem Statement as is from Leetcode 
Given a string s which consists of lowercase or uppercase letters, return the length of the longest palindrome that can be built with those letters.

Letters are case sensitive, for example, "Aa" is not considered a palindrome.

- Example 1:

Input: s = "abccccdd"

Output: 7

Explanation: One longest palindrome that can be built is "dccaccd", whose length is 7.

- Example 2:

Input: s = "a"

Output: 1

Explanation: The longest palindrome that can be built is "a", whose length is 1.

## Explanation

or every character that we encounter in the string having even frequency, no problem using it to construct the palindrome. This is trivial to understand, as even frequency means we can choose 2 positions and place it on each of them — one on the left and one on the right, preserving the symmetry.

The consideration arises when a character has odd frequency. For characters with odd frequency:

We can use (frequency - 1) characters in the palindrome (since that's even).

The one leftover character can’t be mirrored, but it can be placed in the center of the palindrome.

Since a palindrome can have at most one character in the center that doesn’t need a mirrored counterpart, we can only use one odd-frequency character fully. For all other characters with odd counts, we only use the even part.

## Code

The algorithm follows this way. We create a set of characters as it doesn't care about frequency. Whenever we encounter a character for the first time, that means we've seen it once, and to us, it's frequency is 1 which is odd. Hence we do not modify `res` we just add it to the set. When we encounter a character such that we've seen it before (that is, the character is present in the set), we know that we've seen it for the 2nd time (2nd time, 2 is even number) therefore we increment `res` by 2. We also remove it from the set. 

So basically what happens is everytime we see that a charcter has occured for even number of times, i.e., 2, we update res to res + 2. For odd characters, we take the even part of their frequency and if any is left over, then we check if f is empty or not. If f is not empty outside the loop it means some character has occured odd times of which we have taken the even part to make the palindrome, now we can take one of the odd characters remaining for the centre unmirrored element. Hence we check if f is not empty then `res = res + 1` and return `res` accordingly.

```cpp
class Solution {
public:
    int longestPalindrome(string s) {
        set<char> f;
        int res = 0;
        for(char ch: s){
            if(f.count(ch)) {
                f.erase(ch);
                res+=2;
            } else {
                f.insert(ch);
            }
        }
        if(!f.empty()) res++;
        return res;
    }
};
```

## Tags

Greedy