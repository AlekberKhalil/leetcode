# Shortest Way to Form String

From any string, we can form asubsequenceof that string by deleting some number of characters \(possibly no deletions\).

Given two strings`source`and`target`, return the minimum number of subsequences of`source`such that their concatenation equals`target`. If the task is impossible, return`-1`.

**Example 1:**

```text
Input: source = "abc", target = "abcbc"Output: 2Explanation: The target "abcbc" can be formed by "abc" and "bc", which are subsequences of source "abc".
```

**Example 2:**

```text
Input: source = "abc", target = "acdbc"Output: -1Explanation: The target string cannot be constructed from the subsequences of source string due to the character "d" in target string.
```

**Example 3:**

```text
Input: source = "xyz", target = "xzyxz"Output: 3Explanation: The target string can be constructed as follows "xz" + "y" + "xz".
```

**Note:**

1. Both the

   `source`

   and

   `target`

   strings consist of only lowercase English letters from "a"-"z".

2. The lengths of

   `source`

   and

   `target`

   string are between

   `1`

   and

   `1000`

   .

分析

贪心算法

每次遍历完整个source，target有 == 的就移动。下次继续继续重新遍历source。 返回遍历完多少次source

```text
class Solution:    def shortestWay(self, s: str, t: str) -> int:        n,m = len(s),len(t)        res =i= 0        while i < m:            ti = i            for c in s:                if i < m and c == t[i]:                    i += 1            if ti == i:                return -1            res += 1        return res
```

建inverted index:

这里i 其实可以当做source无限连接，i在source的Pos.在reverted Index list范围内就可以跳动，说明还在当前s内，范围外就重来再新一个s继续loop

```text
Initialize i = -1 (i represents the smallest valid next offset) and loop_cnt = 1 (number of passes through source).Iterate through the target
```

[https://leetcode.com/problems/shortest-way-to-form-string/discuss/304662/Python-O\(M-%2B-N\*logM\)-using-inverted-index-%2B-binary-search-\(Similar-to-LC-792\](https://leetcode.com/problems/shortest-way-to-form-string/discuss/304662/Python-O%28M-%2B-N*logM%29-using-inverted-index-%2B-binary-search-%28Similar-to-LC-792%29\)

```text
class Solution:    def shortestWay(self, s: str, t: str) -> int:        ii = collections.defaultdict(list) #invertedIndex        for idx, v in enumerate(s):            ii[v].append(idx)        loopcnt = 1        curidx = -1        for tidx, tv in enumerate(t):            if tv not in ii:                return -1            iidx = bisect.bisect_left(ii[tv],curidx)            if iidx >= len(ii[tv]):                loopcnt += 1                curidx = ii[tv][0] + 1            else:                curidx = ii[tv][iidx] + 1        return loopcnt
```

