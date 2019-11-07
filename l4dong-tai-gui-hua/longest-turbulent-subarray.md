# Longest Turbulent Subarray



A subarray `A[i], A[i+1], ..., A[j]` of `A` is said to be _turbulent_ if and only if:

* For `i <= k < j`, `A[k] > A[k+1]` when `k` is odd, and `A[k] < A[k+1]` when `k` is even;
* **OR**, for `i <= k < j`, `A[k] > A[k+1]` when `k` is even, and `A[k] < A[k+1]` when `k` is odd.

That is, the subarray is turbulent if the comparison sign flips between each adjacent pair of elements in the subarray.

Return the **length** of a maximum size turbulent subarray of A.

**Example 1:**

```text
Input: [9,4,2,10,7,8,8,1,9]Output: 5Explanation: (A[1] > A[2] < A[3] > A[4] < A[5])
```

**Example 2:**

```text
Input: [4,8,12,16]Output: 2
```

**Example 3:**

```text
Input: [100]Output: 1
```

**Note:**

1. `1 <= A.length <= 40000`
2. `0 <= A[i] <= 10^9`

分析：

若弯曲则up由down来，down由up来，这样其实一直保存了最大曲线的长度且递增，同时也保存了当前现状。

loop里每次res也更新得到最大。

```text
class Solution:    def maxTurbulenceSize(self, A: List[int]) -> int:        n = len(A)        up,down,res=1,1,1        for i in range(1,n):            if A[i] > A[i-1]:                up = down+1                down =1            elif A[i] < A[i-1]:                down = up+1                up = 1            else:                up=down=1            res = max(res,up,down)        return res
```

