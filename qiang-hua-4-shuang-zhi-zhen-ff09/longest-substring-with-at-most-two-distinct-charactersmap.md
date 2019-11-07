# Longest Substring with At Most Two Distinct Characters\(map\)

Given a string_**s**_, find the length of the longest substring \_**t** \_that contains**at most**2 distinct characters.

**Example 1:**

```text
Input:
 "eceba"

Output: 
3

Explanation: 
t
is "ece" which its length is 3.
```

**Example 2:**

```text
Input:
 "ccaabbb"

Output: 
5

Explanation: 
t
is "aabbb" which its length is 5.
```

分析

用模板

```text
class Solution:
    def lengthOfLongestSubstringTwoDistinct(self, s: str) -> int:
        mmap = collections.defaultdict(int)
        ss=e=d=counter = 0
        l = len(s)


        while e < l:
            if mmap[s[e]] == 0:
                counter += 1
            mmap[s[e]] += 1
            e += 1
            while counter > 2:
                if mmap[s[ss]] == 1:
                    counter -= 1
                mmap[s[ss]] -= 1
                ss += 1
            d = max(d, e - ss)
        return d
```

