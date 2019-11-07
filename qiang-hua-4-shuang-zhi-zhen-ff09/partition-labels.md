# Partition Labels

A string`S`of lowercase letters is given. We want to partition this string into as many parts as possible so that each letter appears in at most one part, and return a list of integers representing the size of these parts.

**Example 1:**

```text
Input: S = "ababcbacadefegdehijhklij"Output: [9,7,8]Explanation:The partition is "ababcbaca", "defegde", "hijhklij".This is a partition so that each letter appears in at most one part.A partition like "ababcbacadefegde", "hijhklij" is incorrect, because it splits S into less parts.
```

**Note:**

```text
S will have length in range [1, 500].S will consist of lowercase letters ('a' to 'z') only.
```

分析

自己做法：双指针，counter Str和辅助set。 counter == len\(set\)就可以断开一段，s=e重新开始

```text
class Solution:    def partitionLabels(self, S: str) -> List[int]:        mm = collections.Counter(list(S))        cnt=s=e=0        l = len(S)        ss = set()        res = []        while e < l:            if mm[S[e]] == 1:                cnt += 1            ss.add(S[e])            mm[S[e]] -= 1            e += 1            if cnt == len(ss):                res.append(e-s)                s = e                ss = set()                cnt = 0        return res
```

类似贪心法

这个区间内所有数最大的范围作为last。i到了那个last就是一段。

```text
class Solution:    def partitionLabels(self, S: str) -> List[int]:        mm = {}        for i,v in enumerate(S):            mm[v] = i        ll = len(S)        s = last = 0        res = []        for i in range(ll):            last = max(last, mm[S[i]])#类似贪心算法，这个区间内所有数最大的范围作为last。到了那个last就是一段            if i == last:                res.append(last - s + 1)                s = last + 1        return res
```

