# Jump Game

Given an array of non-negative integers, you are initially positioned at the first index of the array.

Each element in the array represents your maximum jump length at that position.

Determine if you are able to reach the last index.

For example:  
A =`[2,3,1,1,4]`, return`true`.

A =`[3,2,1,0,4]`, return`false`.

分析

贪心法,max是当前能走到最远的距离，小于当前i就不行。

```text
class Solution {
    public boolean canJump(int[] nums) {
        if(nums.length == 0)
            return true;
        int max = 0;
        for(int i = 0; i < nums.length; i ++){            
            if(max < i) //这步不能漏啊 要不走下去到最后肯定都true
                return false;
            max = Math.max(max, i + nums[i]);
        }

            return max >= nums.length - 1;
    }
}
```

dp做法

```text
class Solution:
    def canJump(self, nums):
        """
        :type nums: List[int]
        :rtype: bool
        """
        if not nums:
            return False
        n = len(nums)
        f = [False]*n
        f[0]=True
        for i in range(1,n):
            for j in range(i):
                if f[j] and j + nums[j] >= i:
                    f[i] = True
                    break
        return f[n-1]
```

