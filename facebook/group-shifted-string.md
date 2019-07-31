# Group Shifted String

Given an array of strings \(all lowercase letters\), the task is to group them in such a way that all strings in a group are shifted versions of each other. Two string S and T are called shifted if,

```text
S.length = T.length 
and
S[i] = T[i] + K for 
1 
<
= i 
<
= S.length  for a constant integer K
```

For example strings {acd, dfg, wyz, yab, mop} are shifted versions of each other.

```text
Input  : str[] = {"acd", "dfg", "wyz", "yab", "mop",
                 "bdfh", "a", "x", "moqs"};

Output : a x
         acd dfg wyz yab mop
         bdfh moqs
All shifted strings are grouped together.
```

分析

```text
a c d -> 2 1
d f g -> 2 1
m o p -> 2 1
```

一组里的数之间diff相等，所以每个str都算出来c-&gt;c diff,比如2，1.为了好做存成‘ab'

map: diff -&gt; list of strs

```text
import collections
class Solution:
    def getDiff(self,str):
        n = len(str)
        diff = []
        for i in range(1,n):
            d = ord(str[i])-ord(str[i-1])
            d = chr(d+ord('a')) if d > 0 else chr(26+d+ord('a'))
            diff.append(d)
        return ''.join(diff)

    def groupShiftedString(self,strs):

        map = collections.defaultdict(list)
        for s in strs:
            map[self.getDiff(s)].append(s)
        res = [i for i in map.values()]
        return res
```

