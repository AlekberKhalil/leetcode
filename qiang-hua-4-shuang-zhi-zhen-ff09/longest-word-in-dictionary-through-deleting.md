# Longest Word in Dictionary through Deleting

Given a string and a string dictionary, find the longest string in the dictionary that can be formed by deleting some characters of the given string. If there are more than one possible results, return the longest word with the smallest lexicographical order. If there is no possible result, return the empty string.

**Example 1:**

```text
Input:s = "abpcplea", d = ["ale","apple","monkey","plea"]Output:"apple"
```

**Example 2:**

```text
Input:s = "abpcplea", d = ["a","b","c"]Output:"a"
```

分析

就是loo字典里每个word，然后每个word和s比较，2个指针一个在word 一个在s 同时出发

这里不用map 因为会乱序，本体要求Order

```text
class Solution:    def findLongestWord(self, s: str, d: List[str]) -> str:        ll = len(s)        maxLen,res = 0,''        for p in d:            ps=pp=0            lp = len(p)            while ps < ll and pp < lp:                if p[pp] == s[ps]:                    pp += 1                ps += 1            if pp == lp:                if maxLen < lp:                    maxLen = lp                    res = p                elif maxLen == lp:                    if res > p:                        res = p                       return res
```

