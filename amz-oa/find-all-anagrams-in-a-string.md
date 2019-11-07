# Find All Anagrams in a String

Given a string **s** and a **non-empty** string **p**, find all the start indices of **p**'s anagrams in **s**.

Strings consists of lowercase English letters only and the length of both strings **s** and **p** will not be larger than 20,100.

The order of output does not matter.

**Example 1:**

```text
Input:s: "cbaebabacd" p: "abc"Output:[0, 6]Explanation:The substring with start index = 0 is "cba", which is an anagram of "abc".The substring with start index = 6 is "bac", which is an anagram of "abc".
```

**Example 2:**

```text
Input:s: "abab" p: "ab"Output:[0, 1, 2]Explanation:The substring with start index = 0 is "ab", which is an anagram of "ab".The substring with start index = 1 is "ba", which is an anagram of "ab".The substring with start index = 2 is "ab", which is an anagram of "ab".
```

分析

追击型指针

这里注意count是distinct 的字符长度

```text
class Solution:    def findAnagrams(self, s: str, p: str) -> List[int]:        l=r=0        mm = {i:0 for i in p}        for i in p:            mm[i] += 1        ll = len(s)        cnt = len(mm)        res = []        while r < ll:            if s[r] in mm:                mm[s[r]] -= 1                if mm[s[r]] == 0:                    cnt -= 1            r += 1            while not cnt:                 if r - l == len(p):                    res.append(l)                if s[l] in mm:                    mm[s[l]] += 1                    if  mm[s[l]] == 1: cnt += 1                                l += 1                                        return res                 
```

