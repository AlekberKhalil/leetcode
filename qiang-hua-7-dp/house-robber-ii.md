# House Robber II

You are a professional robber planning to rob houses along a street. Each house has a certain amount of money stashed. All houses at this place are**arranged in a circle.**That means the first house is the neighbor of the last one. Meanwhile, adjacent houses have security system connected and **it will automatically contact the police if two adjacent houses were broken into on the same night**.

Given a list of non-negative integers representing the amount of money of each house, determine the maximum amount of money you can rob tonight**without alerting the police**.

**Example 1:**

```text
Input: [2,3,2]Output: 3Explanation: You cannot rob house 1 (money = 2) and then rob house 3 (money = 2),             because they are adjacent houses.
```

**Example 2:**

```text
Input: [1,2,3,1]Output: 4Explanation: Rob house 1 (money = 1) and then rob house 3 (money = 3).             Total amount you can rob = 1 + 3 = 4.
```

分析

拆环：1.去头一个数组，去尾一个数组 2.double数组，然后一个window，长度是数组长度

注意这里yes 和No交换进行的方法

```text
class Solution:    def rob(self, nums):        """        :type nums: List[int]        :rtype: int        """        if not nums:            return 0        n = len(nums)        if n == 1:            return nums[0]        nums1 = nums[:n-1]        nums2 = nums[1:]        f1 = self.canDo(nums1)        f2 = self.canDo(nums2)        return max(f1,f2)    def canDo(self, nums):                r = len(nums)        ppre=pre=cur = 0        for i in range(r):            cur = max(pre,ppre+nums[i])            ppre,pre = pre,cur        return cur
```

