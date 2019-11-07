# Longest Mountain in Array

Let's call any \(contiguous\) subarray B \(of A\) a\_mountain\_if the following properties hold:

```text
B.length >= 3There exists some 0 < i < B.length - 1 such that B[0] < B[1] < ... B[i-1] < B[i] > B[i+1] > ... > B[B.length - 1]
```

\(Note that B could be any subarray of A, including the entire array A.\)

Given an array`A` of integers, return the length of the longest _mountain_.

Return`0`if there is no mountain.

**Example 1:**

```text
Input: [2,1,4,7,3,2,5]Output: 5Explanation: The largest mountain is [1,4,7,3,2] which has length 5.
```

**Example 2:**

```text
Input: [2,2,2]Output: 0Explanation: There is no mountain.
```

**Note:**

```text
0 <= A.length <= 100000 <= A[i] <= 10000
```

**Follow up:**

* Can you solve it using only one pass?
* Can you solve it in`O(1)`space?

分析

可以forward backward遍历，2个数组up and down，最后遍历一遍相加。反向遍历也是按照递增来做

```text
class Solution:    def longestMountain(self, A: List[int]) -> int:        maxl = 0        ll = len(A)        up = [0]*ll        down = [0]*ll        for i in range(1,ll):            if A[i] > A[i-1]: up[i] = up[i-1] + 1        for i in reversed(range(ll-1)):            if A[i] > A[i+1]: down[i] = down[i+1] + 1        return  max([u+d+1 for u,d in zip(up,down) if u and d] or [0])
```

或者直接up,down2个变量，一次遍历，遇到不合条件：1 down&gt;0 and 开始增加 2 ==

起始点为0，高/低一个就加1

```text
class Solution:    def longestMountain(self, A: List[int]) -> int:        maxl = up=down=0        ll = len(A)        for i in range(1,ll):            if (down and A[i] >= A[i-1]) or (up and A[i] == A[i-1]):                up = down = 0            up += A[i] > A[i-1] #巧妙用法            down += A[i] < A[i-1]            if up and down:maxl = max(maxl, up + down +1) #注意一定要同时>0才行        return maxl
```

