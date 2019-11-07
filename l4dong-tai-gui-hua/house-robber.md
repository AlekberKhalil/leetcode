# House Robber

You are a professional robber planning to rob houses along a street. Each house has a certain amount of money stashed, the only constraint stopping you from robbing each of them is that adjacent houses have security system connected and**it will automatically contact the police if two adjacent houses were broken into on the same night**.

Given a list of non-negative integers representing the amount of money of each house, determine the maximum amount of money you can rob tonight**without alerting the police**.

**Example 1:**

```text
Input: [1,2,3,1]Output: 4Explanation: Rob house 1 (money = 1) and then rob house 3 (money = 3).             Total amount you can rob = 1 + 3 = 4.
```

**Example 2:**

```text
Input: [2,7,9,3,1]Output: 12Explanation: Rob house 1 (money = 2), rob house 3 (money = 9) and rob house 5 (money = 1).             Total amount you can rob = 2 + 9 + 1 = 12.
```

分析

dp取得是当前最大，所以要延续前面最大的，可能是f\[i-2\]+nums\[i\]或者是f\[i-1\]，哪个大选哪个

```text
class Solution:    def rob(self, nums):        """        :type nums: List[int]        :rtype: int        """        if not nums:            return 0        n = len(nums)        if n <2:            return max(nums)        pp = nums[0]        p = max(nums[0],nums[1])        for i in range(2,n):            cur = max(pp+ nums[i],p)            p,pp = cur,p        return p
```

python可以直接prev和cur一起赋值，所以这里prev是前天，cur是昨天。用前两天的算今天的

```text
class Solution:    def rob(self, nums: List[int]) -> int:        prev=cur=0        for i in nums:            prev,cur = cur, max(prev+i,cur)        return cur
```

