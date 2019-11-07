# Largest Divisible Subset

Given a set of**distinct**positive integers, find the largest subset such that every pair \(Si, Sj\) of elements in this subset satisfies:

Si% Sj= 0 or Sj% Si= 0.

If there are multiple solutions, return any subset is fine.

**Example 1:**

```text
Input: [1,2,3]Output: [1,2] (of course, [1,3] will also be ok)
```

**Example 2:**

```text
Input: [1,2,4,8]Output: [1,2,4,8]
```

分析

因为需要返回List,这里2个dp，count 以i结尾的list, pre记载前数的数组

一个count count\[i\]&lt;count\[j\]+1就可以更新。每次只需要比较旧数组里最后元素j是否能被新加入i %，不需要遍历旧数组所有元素

```text
class Solution:    def largestDivisibleSubset(self, nums: List[int]) -> List[int]:        n = len(nums)        count = [0]*(n)        pre = [-1]*(n)        maxlen,index = float('-inf'),-1        nums.sort()#要排序        for i in range(n):            for j in range(i-1,-1,-1):                if nums[i]%nums[j]==0 and count[j]+1>count[i]:#只要能%最后元素j就行，不必所有元素都%.                    count[i] = count[j]+1                    pre[i] = j            if count[i] > maxlen:                maxlen = count[i]                index = i        res = []        while index!=-1:            res.append(nums[index])            index = pre[index]                    return res
```

用set慢慢扩展

```text
class Solution:    def largestDivisibleSubset(self, nums: List[int]) -> List[int]:        n = len(nums)        count = [0]*(n)        pre = [-1]*(n)        maxlen,index = float('-inf'),-1        nums.sort()#要排序        s = {-1:set()}        for x in nums:            s[x] = max((s[d] for d in s if x%d == 0),key = len)|{x}        return list(max(s.values(),key = len))
```

