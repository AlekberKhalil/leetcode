# Longest Substring with At Most K Distinct Characters\(模板）

## Longest Substring with At Most K Distinct Characters

Given a string_s_, find the length of the longest substring T that contains at most k distinct characters.

## Example

For example, Given s =`"eceba"`,`k = 3`,

T is`"eceb"`which its length is`4`.

## Challenge

O\(n\), n is the size of the string_s_.

分析

count 记录distinct 数目，所以是 while cnt &gt; k

start的while 条件是while counter&gt;k 不是counter+=k

```text
import collections


class Solution:
    """
    @param s: A string
    @param k: An integer
    @return: An integer
    """
    def lengthOfLongestSubstringKDistinct(self, s, k):
        # write your code here
        counter = start = end = d = 0
        map = collections.defaultdict(int)
        n = len(s)
        while end < n:
            if map[s[end]]==0:
                counter +=1
            map[s[end]]+=1
            end +=1
            while counter > k:
                if map[s[start]]==1:
                    counter -=1
                map[s[start]] -=1
                start +=1
            d = max(d,end-start)
        return d
```

