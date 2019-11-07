# Maximum Length of Pair Chain

You are given`n`pairs of numbers. In every pair, the first number is always smaller than the second number.

Now, we define a pair`(c, d)`can follow another pair`(a, b)`if and only if`b < c`. Chain of pairs can be formed in this fashion.

Given a set of pairs, find the length longest chain which can be formed. You needn't use up all the given pairs. You can select pairs in any order.

**Example 1:**

```text
Input: [[1,2], [2,3], [3,4]]Output: 2Explanation: The longest chain is [1,2] -> [3,4]
```

**Note:**

1. The number of given pairs will be in the range \[1, 1000\].

分析

因为可以任意顺序，但是每个Pair first&lt;second，先排序

dp表示到当前i 最长的chain， 2层循环，为了及时返回，第二层倒序。

```text
class Solution:    def findLongestChain(self, pairs: List[List[int]]) -> int:        n = len(pairs)        f = [1]*(n+1)        res = 0        # for i in range(1,n+1):        #     f[i] = 1        pairs.sort()        for i in range(1,n+1):                        for j in range(i-1,-1,-1): #倒序是为了及时break 防止TLE                ca,cb = pairs[i-1]                pa,pb = pairs[j-1]                if ca > pb:                    f[i]  = max(f[i],f[j] + 1)                    break            res = max(res,f[i])        return res
```

按照end排序，然后一个个数顺移计算res

不按start，因为可能第一个数范围就涵盖了后面所有数，导致结果是1，具体解释：

[https://leetcode.com/problems/maximum-length-of-pair-chain/discuss/105607/4-Liner-Python-Greedy](https://leetcode.com/problems/maximum-length-of-pair-chain/discuss/105607/4-Liner-Python-Greedy)

```text
class Solution:    def findLongestChain(self, pairs: List[List[int]]) -> int:        pairs.sort(key = lambda x: (x[1],x[0]))#记得要加括号！！！！        pre = float('-inf')        res = 0        for a, b in pairs:            if pre < a:                pre,res = b,res+1        return res
```

