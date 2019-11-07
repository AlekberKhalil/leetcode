# Longest Substring with At Least K Repeating Characters\(区别）

Find the length of the longest substring**T**of a given string \(consists of lowercase letters only\) such that every character in**T**appears no less thanktimes.

**Example 1:**

```text
Input:s = "aaabb", k = 3Output:3The longest substring is "aaa", as 'a' is repeated 3 times.
```

**Example 2:**

```text
Input:s = "ababbc", k = 2Output:5The longest substring is "ababb", as 'a' is repeated 2 times and 'b' is repeated 3 times.
```

双指针模板没做出来，用递归

找出count&lt;k的char,用来做分隔符把str分成2段，继续递归。最后记得返回len\(s\)

```text
class Solution:    def longestSubstring(self, s, k):        """        :type s: str        :type k: int        :rtype: int        """        for i in set(s):            if s.count(i)<k:                return max(self.longestSubstring(x,k) for x in s.split(i))        return len(s)
```

