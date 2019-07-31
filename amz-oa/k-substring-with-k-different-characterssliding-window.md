# K-Substring with K different characters\(sliding window\)

## Description

Given a string S and an integer K.  
Calculate the number of substrings of length K and containing K different characters

Have you met this question in a real interview?

Yes

Problem Correction

## Example

```text
String: "abcabc"
K: 3

Answer: 3
substrings:  ["abc", "bca", "cab"]
```

```text
String: "abacab"
K: 3

Answer: 2
substrings: ["bac", "cab"]
```

分析

for 里面I做end指针，直接用i-k，不用start指针了。

几大元素：start, end, map, count, size of substring\(maybe\)

这里count检测map进入1和退出0的情况，然后++ --

这里需要set 为了去重 比如重复出现的ab

```text
class Solution:
    """
    @param stringIn: The original string.
    @param K: The length of substrings.
    @return: return the count of substring of length K and exactly K distinct characters.
    """
    import collections
    def KSubstring(self, stringIn, K):
        # Write your code here
        map = collections.defaultdict(int)
        i=j=0
        cnt = 0
        res = set()
        strLen = len(stringIn)
        for i in range(strLen):
            c = stringIn[i]
            map[c] += 1
            if map[c] == 1:
                cnt += 1
            if i >= K:
                c = stringIn[i - K]
                map[c] -= 1
                if map[c] == 0:
                    cnt -= 1
            if cnt == K:
                res.add(stringIn[i - K + 1:i + 1])
        return len(res)
```

