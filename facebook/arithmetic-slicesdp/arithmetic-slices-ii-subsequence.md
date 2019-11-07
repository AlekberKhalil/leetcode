# Arithmetic Slices II - Subsequence

A sequence of numbers is called arithmetic if it consists of at least three elements and if the difference between any two consecutive elements is the same.

For example, these are arithmetic sequences:

```text
1, 3, 5, 7, 9
7, 7, 7, 7
3, -1, -5, -9
```

The following sequence is not arithmetic.

```text
1, 1, 2, 5, 7
```

A zero-indexed array A consisting of N numbers is given. A**subsequence**slice of that array is any sequence of integers \(P0, P1, ..., Pk\) such that 0 ≤ P0&lt; P1&lt; ... &lt; Pk&lt; N.

A**subsequence**slice \(P0, P1, ..., Pk\) of array A is called arithmetic if the sequence A\[P0\], A\[P1\], ..., A\[Pk-1\], A\[Pk\] is arithmetic. In particular, this means that k ≥ 2.

The function should return the number of arithmetic subsequence slices in the array A.

The input contains N integers. Every integer is in the range of -231and 231-1 and 0 ≤ N ≤ 1000. The output is guaranteed to be less than 231-1.

**Example:**

```text
Input:
 [2, 4, 6, 8, 10]


Output:
 7


Explanation:

All arithmetic subsequence slices are:
[2,4,6]
[4,6,8]
[6,8,10]
[2,4,6,8]
[4,6,8,10]
[2,4,6,8,10]
[2,6,10]
```

分析

和ii的区别是这里数要连续不能打断，ii可以任意的sequence数组合，一旦打断cur = 0

这里是dict的数组，arr\[i\]=\[dict\*n\] dict = {diff:count}

这里也是做2件事，一个update ans，就是ans+=f\[j-1\] 另一个就是Update f\[j\]+=1+f\[j\]

```text
import collections


class Solution:
    def numberOfArithmeticSlices(self, A):
        """
        :type A: List[int]
        :rtype: int
        """
        n = len(A)
        f = []
        res = 0

        for i in range(n):
            f.append(collections.defaultdict(int))
            for j in range(i):
                d = A[i]-A[j]
                f[i][d]+=1    #和j形成新的length=2的等差数组，所以无论如何加1            
                if d in f[j]:               
                    res += f[j][d] #加入A[i]只是让f[j]里所有arr的长度都++，arr count还是没变。但是所有arr有新元素都更新了，所以res要加上当前的arr count
                    f[i][d] +=f[j][d]
        return res
```

