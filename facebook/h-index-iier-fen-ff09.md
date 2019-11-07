# H-Index II\(二分）

Given an array of citations**sorted in ascending order**\(each citation is a non-negative integer\) of a researcher, write a function to compute the researcher's h-index.

According to the [definition of h-index on Wikipedia](https://en.wikipedia.org/wiki/H-index): "A scientist has index h if h of his/her N papers have **at least**h citations each, and the other N − h papers have **no more than**h citations each."

**Example:**

```text
Input:citations = [0,1,3,5,6]Output: 3 Explanation: [0,1,3,5,6] means the researcher has 5 papers in total and each of them had              received 0, 1, 3, 5, 6 citations respectively.              Since the researcher has 3 papers with at least3 citations each and the remaining              two with no more than3 citations each, her h-index is 3.
```

**Note:**

If there are several possible values for _h_, the maximum one is taken as the h-index.

**Follow up:**

* This is a follow up problem to 

  [H-Index](https://leetcode.com/problems/h-index/description/)

  , where

  `citations`

  is now guaranteed to be sorted in ascending order.

* Could you solve it in logarithmic time complexity?

分析

用标准二分模板做。记得条件是num\[m\]&gt;=n-m（长度）

H-index I完全一样，就是需要排序而已

```text
class Solution:    def hIndex(self, citations):        """        :type citations: List[int]        :rtype: int        """        n = len(citations)        if n == 0:            return 0        s, e = 0, n - 1        while s + 1 < e:            m = s + (e - s) // 2            if n-m <= citations[m]:                e = m            else:                s = m        if n-s <= citations[s]:            return n-s        if n-e <= citations[e]:            return n-e        return 0
```

