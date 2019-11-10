# Longest Common Prefix



Write a function to find the longest common prefix string amongst an array of strings.

If there is no common prefix, return an empty string `""`.

**Example 1:**

```text
Input: ["flower","flow","flight"]
Output: "fl"
```

**Example 2:**

```text
Input: ["dog","racecar","car"]
Output: ""
Explanation: There is no common prefix among the input strings.
```

分析

按照长度排序 sort\(key=len\),取第一个str和后面所有str 按照index一个个比，第一个不等的就是最短长度

```text
class Solution:
    def longestCommonPrefix(self, strs: List[str]) -> str:
        if not strs:
            return ''
        strs.sort(key=len)
        cur = strs[0]
        for i,s in enumerate(cur):
            for others in strs[1:]:
                if others[i]!=s:
                    return cur[:i]
        return cur
            
        
```

