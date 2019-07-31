# First Unique Character in a String

Given a string, find the first non-repeating character in it and return it's index. If it doesn't exist, return -1.

**Examples:**

```text
s = "leetcode"
return 0.

s = "loveleetcode",
return 2.
```

分析

dict 存 i: count， 第二次loop遇到count==1直接返回Index

```text
import collections


class Solution:
    def firstUniqChar(self, s):
        """
        :type s: str
        :rtype: int
        """
        count = collections.defaultdict(int)
        for i in s:
            count[i] += 1
        for i,v in enumerate(s):
            if count[v] == 1:
                return i
        return -1
```

python 法 注意 min\(\[\] or\[-1\]\)

```text
min([s.index(char) for char in set(s) if s.count(char) == 1] or [-1])
```

