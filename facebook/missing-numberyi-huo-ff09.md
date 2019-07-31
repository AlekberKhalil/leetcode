# Missing Number\(异或）

Given an array containingndistinct numbers taken from`0, 1, 2, ..., n`, find the one that is missing from the array.

**Example 1:**

```text
Input:
 [3,0,1]

Output:
 2
```

**Example 2:**

```text
Input:
 [9,6,4,2,3,5,7,0,1]

Output:
 8
```

**Note**:  
Your algorithm should run in linear runtime complexity. Could you implement it using only constant extra space complexity?

分析

异或 x=x^index^nums\[index\] 完美数组的数组 index=nums\[index\]

或者n\(n+1\)//2 记得要用//2

```text
class Solution:
    def missingNumber(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """

        # xor=len(nums)
        # for i in range(len(nums)):
        #     xor = xor^i^nums[i]
        # return xor


        n = len(nums)
        return n*(n+1)//2 -sum(nums)
```

