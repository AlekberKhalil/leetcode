# Longest Repeating Character Replacement

Given a string that consists of only uppercase English letters, you can replace any letter in the string with another letter at most k times. Find the length of a longest substring containing all repeating letters you can get after performing the above operations.

#### Example

**Example1**

```text
Input:"ABAB"2Output:4Explanation:Replace the two 'A's with two 'B's or vice versa.
```

**Example2**

```text
Input:"AABABBA"1Output:4Explanation:Replace the one 'A' in the middle with 'B' and form "AABBBBA".The substring "BBBB" has the longest repeating letters, which is 4.
```

#### Notice

Both the string's length and k will not exceed 10^4.

分析

双指针模板，right++，charcnt\[left\] + k &lt; right - left +1 移动Left

```text
class Solution:    """    @param s: a string    @param k: a integer    @return: return a integer    """    def characterReplacement(self, s, k):        # write your code here               l = 0        charcnt = collections.defaultdict(int)        res= 0        for r in range(len(s)):            charcnt[s[r]] += 1                        while k + charcnt[s[l]]  < r - l + 1:                charcnt[s[l]] -= 1                l += 1            res = max(res, r-l+1)        return res            
```

