# Interval List Intersections

Given two lists of**closed**intervals, each list of intervals is pairwise disjoint and in sorted order.

Return the intersection of these two interval lists.

_\(Formally, a closed interval`[a, b]`\(with`a <= b`\) denotes the set of real numbers`x`with`a <= x <= b`. The intersection of two closed intervals is a set of real numbers that is either empty, or can be represented as a closed interval. For example, the intersection of \[1, 3\] and \[2, 4\] is \[2, 3\].\)_

**Example 1:**

![](https://assets.leetcode.com/uploads/2019/01/30/interval1.png)

```text
Input: A = [[0,2],[5,10],[13,23],[24,25]], B = [[1,5],[8,12],[15,24],[25,26]]Output: [[1,2],[5,5],[8,10],[15,23],[24,24],[25,25]]Reminder: The inputs and the desired output are lists of Interval objects, and not arrays or lists.
```

**Note:**

```text
0 <= A.length < 10000 <= B.length < 10000 <= A[i].start, A[i].end, B[i].start, B[i].end < 10^9
```

分析

two pointer

A,B各捡一段取maxhead和Mintail。不为空就是交集，加入res

然后哪个end小放弃那段，一样小一起放弃

```text
class Solution:    def intervalIntersection(self, A: List[List[int]], B: List[List[int]]) -> List[List[int]]:        res = []        a = b = 0        while a<len(A) and b <len(B):            tail = min(A[a][1], B[b][1])            head = max(A[a][0], B[b][0])            if head <= tail:                res.append([head,tail]) #有交集就加入            #哪个end小就放弃，一样的话一起放弃            if A[a][1] == tail:                a += 1            if B[b][1] == tail:                b += 1        return res
```

