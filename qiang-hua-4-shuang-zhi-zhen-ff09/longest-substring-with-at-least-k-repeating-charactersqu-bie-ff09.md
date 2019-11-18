# Longest Substring with At Least K Repeating Characters\(区别）

Find the length of the longest substring**T**of a given string \(consists of lowercase letters only\) such that every character in**T**appears no less thanktimes.

**Example 1:**

```text
Input:
s = "aaabb", k = 3

Output:
3

The longest substring is "aaa", as 'a' is repeated 3 times.
```

**Example 2:**

```text
Input:
s = "ababbc", k = 2

Output:
5

The longest substring is "ababb", as 'a' is repeated 2 times and 'b' is repeated 3 times.
```



双指针

双指针做26次，1-27每次代表有几个unique char，保证每个unique char的frequency 》= k. 

每次双指针， s, e记录2个 \# of unique chars && \# of char more than K

如果这俩\# == 当前数字 1-27, 是个可行解，比较计算max。

```text
import string
class Solution:
    def longestSubstring(self, s: str, k: int) -> int:
        
        res= 0
        n = len(s)
        for u in range(26):
            mm = {key:0 for key in string.ascii_lowercase}
            l=e=0
            numOfUnique = numOfKOrMore = 0
            while e < n:
                if numOfUnique <= u:
                    mm[s[e]] += 1
                    if mm[s[e]] == 1:
                        numOfUnique += 1
                    if mm[s[e]] == k:
                        numOfKOrMore += 1
                    e += 1
                else:
                    mm[s[l]] -= 1
                    if mm[s[l]] == 0:
                        numOfUnique -= 1
                    if mm[s[l]] == k - 1:
                        numOfKOrMore -= 1
                    l += 1
                
                if numOfUnique == u and numOfKOrMore == u:
                    res = max(res, e - l)
        return res
```

用26个位向量，2个loop，头固定尾动。

每个新头新counter和新mask。出现了但不到k的char设为1，满K设为0.最后mask ==0 说明所有出现的char都出现K次，得到一个解。

注意~（1&lt;&lt;i\)按位取反

超时了本作法 [https://leetcode.com/problems/longest-substring-with-at-least-k-repeating-characters/discuss/87749/Two-short-C%2B%2B-solutions-\(3ms-and-6ms\)](https://leetcode.com/problems/longest-substring-with-at-least-k-repeating-characters/discuss/87749/Two-short-C%2B%2B-solutions-%283ms-and-6ms%29)

```text
class Solution:
    def longestSubstring(self, s: str, k: int) -> int:
        first = 0
        n = len(s)        
        res = 0        
        while first <= n-k:
            mm = [0]*26
            mask = 0
            maxLast = first
            for last in range(first,n):
                lastc = s[last]    
                ci = ord(lastc) - ord('a')
                mm[ci] += 1
                if mm[ci] < k:
                    mask |= 1 << ci #不满K设置1
                else:
                    mask &= ~(1 << ci) #满K了设置0
                if mask == 0: #全满K就是合法解
                    res = max(res,last-first+1)  
                    maxLast = last
                
            first = maxLast + 1 #覆盖的str不要考虑
        return res
            
        
```

双指针模板没做出来，用递归

找出count&lt;k的char,用来做分隔符把str分成2段，继续递归。最后记得返回len\(s\)

```text
class Solution:
    def longestSubstring(self, s, k):
        """
        :type s: str
        :type k: int
        :rtype: int
        """

        for i in set(s):
            if s.count(i)<k:
                return max(self.longestSubstring(x,k) for x in s.split(i))

        return len(s)
```



