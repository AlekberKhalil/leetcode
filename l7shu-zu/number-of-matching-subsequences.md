# Number of Matching Subsequences

Given string`S`and a dictionary of words`words`, find the number of`words[i]`that is a subsequence of`S`.

```text
Example :Input:S = "abcde"words = ["a", "bb", "acd", "ace"]Output: 3Explanation: There are three words in words that are a subsequence of S: "a", "acd", "ace".
```

**Note:**

* All words in

  `words`

  and

  `S`

  will only consists of lowercase letters.

* The length of

  `S`

  will be in the range of

  `[1, 50000]`

  .

* The length of

  `words`

  will be in the range of 

  `[1, 5000]`

  .

* The length of

  `words[i]`

  will be in the range of

  `[1, 50]`

  .

分析

类似**Shortest Way to Form String**，建立 Inverted index。在index list内就是存在，&gt;= len\(charlist\)说明不在。同时curidx是在当前source的Pos，每次都要记得更新。

```text
class Solution:    def shortestWay(self, s: str, t: str) -> int:        ii = collections.defaultdict(list) #invertedIndex        for idx, v in enumerate(s):            ii[v].append(idx)        loopcnt = 1        curidx = -1        for tidx, tv in enumerate(t):            if tv not in ii:                return -1            iidx = bisect.bisect_left(ii[tv],curidx)            if iidx >= len(ii[tv]):                loopcnt += 1                curidx = ii[tv][0] + 1            else:                curidx = ii[tv][iidx] + 1        return loopcnt
```

