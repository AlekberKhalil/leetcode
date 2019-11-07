# Arithmetic Slices\(dp\)

A sequence of number is called arithmetic if it consists of at least three elements and if the difference between any two consecutive elements is the same.

For example, these are arithmetic sequence:

```text
1, 3, 5, 7, 9
7, 7, 7, 7
3, -1, -5, -9
```

The following sequence is not arithmetic.

```text
1, 1, 2, 5, 7
```

A zero-indexed array A consisting of N numbers is given. A slice of that array is any pair of integers \(P, Q\) such that 0 &lt;= P &lt; Q &lt; N.

A slice \(P, Q\) of array A is called arithmetic if the sequence:  
A\[P\], A\[p + 1\], ..., A\[Q - 1\], A\[Q\] is arithmetic. In particular, this means that P + 1 &lt; Q.

The function should return the number of arithmetic slices in the array A.

**Example:**

```text
A = [1, 2, 3, 4]

return: 3, for 3 arithmetic slices in A: [1, 2, 3], [2, 3, 4] and [1, 2, 3, 4] itself.
```

分析

和ii的区别是这里数要连续不能打断，ii可以任意的sequence数组合，一旦打断cur = 0

cur追踪了连续\# of 3个数都是arithmetic，当前的f\[j\]=f\[j-1\]+cur

cur = f\[j\]每次新加入数会让原先length=2的变成合法length==3，所以cur+1

同时以前的arr count不变，末尾+new element都变成新arr了，但是count还是和f\[j-1\]一样的,所以sum+=f\[j-1\]

```text
class Solution:
    def numberOfArithmeticSlices(self, A):
        """
        :type A: List[int]
        :rtype: int
        """
        if not A:
            return 0
        sum,cur=0,0
        for j in range(2,len(A)):
            if A[j-1]-A[j-2] == A[j]-A[j-1]:
                cur+=1 #f[i]=cur, 新加入数会让原先==2的变成合法，所以++1，同时以前的arr count不变，末尾+new element都变成新arr了，但是count还是和f[i-1]一样的
                sum+=cur #加入当前的count
            else:
                cur=0
        return sum
```

