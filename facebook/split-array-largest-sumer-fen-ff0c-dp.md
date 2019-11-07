# Split Array Largest Sum\(二分，dp？）

Given an array which consists of non-negative integers and an integerm, you can split the array intomnon-empty continuous subarrays. Write an algorithm to minimize the largest sum among thesemsubarrays.

**Note:**  
If n is the length of array, assume the following constraints are satisfied:

```text
1 ≤ n ≤ 1000
1 ≤ m ≤ min(50, n)
```

**Examples:**

```text
Input:
nums = [7,2,5,10,8]
m = 2

Output:
18

Explanation:
There are four ways to split nums into two subarrays.
The best way is to split it into [7,2,5] and [10,8],
where the largest sum among the two subarrays is only 18.
```

分析：

看成找一个target，使得分成的m个subarray的sum都&lt;=target，所以用二分，这个target在max\(nums\)和sum\(nums）之间。在这个区间左右移动算是已排序数组。

辅助函数中cnt是切下去的刀数。刀数+1 = group数目

这里二分不知道边界怎么做了

```text
class Solution:
    def splitArray(self, nums, m):
        """
        :type nums: List[int]
        :type m: int
        :rtype: int
        """
        l = max(nums)
        r = sum(nums)
        if m == 1:
            return r

        while l < r:
            mid = (l+r)//2
            if self.valid(nums, m, mid):
                r = mid
            else:
                l = mid+1
        return r

    def valid(self,nums,m,target):
        cnt = 0
        summ = 0
        for num in nums:
            summ += num
            if summ > target:
                summ = num
                cnt += 1
                if cnt + 1 > m:
                     return False

        return True
```

dp：前面j组和i结尾，然后j,i之间开始切分最后一组。有点类似背包最后一个value开分。

Python可以 python3不行

```text
class Solution(object):

    def splitArray(self, nums, m):
        if not nums or not m or len(nums) < m:
            return
        n = len(nums)
        f = [float('inf')]*(n+1)
        presum = [0]*(n+1)
        for i,v in enumerate(nums):
            presum[i+1] = presum[i]+v

        f[0]=0
        for i in range(m):
            for j in range(n,0,-1): #1->n
                for k in range(i-1,j):
                    f[j]=min(f[j],max(f[k],presum[j]-presum[k]))

        return f[n]
```

