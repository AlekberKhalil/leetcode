# 3Sum With Multiplicity

Given an integer array`A`, and an integer`target`, return the number of tuples `i, j, k` such that`i < j < k`and `A[i] + A[j] + A[k] == target`.

**As the answer can be very large, return it modulo** `10^9 + 7`.

**Example 1:**

```text
Input: 
A = 
[1,1,2,2,3,3,4,4,5,5]
, target = 
8
Output: 
20
Explanation: 

Enumerating by the values (A[i], A[j], A[k]):
(1, 2, 5) occurs 8 times;
(1, 3, 4) occurs 8 times;
(2, 2, 4) occurs 2 times;
(2, 3, 3) occurs 2 times.
```

**Example 2:**

```text
Input: 
A = 
[1,1,2,2,2,2]
, target = 
5
Output: 
12
Explanation: 

A[i] = 1, A[j] = A[k] = 2 occurs 12 times:
We choose one 1 from [1,1] in 2 ways,
and two 2s from [2,2,2,2] in 6 ways.
```

**Note:**

```text
3 <= A.length <= 3000
0 <= A[i] <= 100
0 <= target <= 300
```

分析

这题是重复的3sum，可以和不重复的3sum做比较。

counter里i j k取值。 一定要记住i&lt;j&lt;k 防止重复

用到排列组合

3个重复数就c32=i\*\(i-1\)\*\(i-2\)/6

3个不重复 就是A32 = i\*\(i-1\)\*\(i-2\)

```text
class Solution:
    def threeSumMulti(self, A: List[int], target: int) -> int:
        c = collections.Counter(A)
        MOD = 10**9 + 7   
        res = 0
        ll = list(c.keys())
        #三个数必须顺序i<j<k 要不有重复
        for i in c.keys():
            for j in c.keys():
                if j > i:
                    continue
                k = target - i - j  
                if i == j == k: res += c[i] * (c[i] - 1) * (c[i] - 2) // 6
                elif i == j != k: res += c[i] * (c[i] - 1) // 2 * c[k]  #不太懂为什么这么不是j<k
                elif k > i and k > j: res += c[i] * c[j] * c[k]


        return res % MOD
```

