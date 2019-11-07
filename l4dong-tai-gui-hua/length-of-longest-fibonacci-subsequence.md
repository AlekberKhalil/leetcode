# Length of Longest Fibonacci Subsequence

A sequence`X_1, X_2, ..., X_n` is\_fibonacci-like\_if:

* `n`

  `>`

  `= 3`

* `X_i + X_{i+1} = X_{i+2}`

   for all 

  `i + 2`

  `<`

  `= n`

Given a**strictly increasing** array `A`of positive integers forming a sequence, find the**length**of the longest fibonacci-like subsequence of`A`. If one does not exist, return 0.

\(_Recall that a subsequence is derived from another sequence`A`by deleting any number of elements \(including none\) from`A`, without changing the order of the remaining elements. For example,`[3, 5, 8]`is a subsequence of`[3, 4, 5, 6, 7, 8]`._\)

* **Example 1:**

```text
Input: [1,2,3,4,5,6,7,8]Output: 5Explanation:The longest subsequence that is fibonacci-like: [1,2,3,5,8].
```

**Example 2:**

```text
Input: [1,3,7,11,12,14,18]Output: 3Explanation:The longest subsequence that is fibonacci-like:[1,11,12], [3,11,14] or [7,11,18].
```

**Note:**

* ```text
  3 <= A.length <= 10001 <= A[0] < A[1] < ... < A[A.length - 1] <= 10^9(The time limit has been reduced by 50% for submissions in Java, C, and C++.)
  ```

分析

任意2个数选出来做起点然后一直走下来。最后选最长的

```text
class Solution:    def lenLongestFibSubseq(self, A: List[int]) -> int:        res = float('-inf')        n = len(A)        ss = set(A)#加快速度        for i in range(n):            for j in range(i+1,n):                a,b,c = A[i],A[j],2                while a+b in ss:                    a,b = b,a+b                    c +=1                res = max(res,c)        return res if res > 2 else 0 #没有的情况
```

