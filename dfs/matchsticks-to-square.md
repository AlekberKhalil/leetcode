# Matchsticks to Square

Remember the story of Little Match Girl? By now, you know exactly what matchsticks the little match girl has, please find out a way you can make one square by using up all those matchsticks. You should not break any stick, but you can link them up, and each matchstick must be used**exactly**one time.

Your input will be several matchsticks the girl has, represented with their stick length. Your output will either be true or false, to represent whether you could make one square using all the matchsticks the little match girl has.

**Example 1:**

```text
Input: [1,1,2,2,2]Output: trueExplanation: You can form a square with length 2, one side of the square came two sticks with length 1.
```

**Example 2:**

```text
Input: [3,3,3,3,4]Output: falseExplanation: You cannot find a way to form a square with all the matchsticks.
```

**Note:**

1. The length sum of the given matchsticks is in the range of

   `0`

   to

   `10^9`

   .

2. The length of the given matchstick array will not exceed

   `15`

分析

把数组分成4个相等的sum

模仿combination sum,除了targetsum变成targestsum\[4\]

数组反向排序加快速度。

```text
class Solution:    def makesquare(self, nums: List[int]) -> bool:        if not nums:            return False        ss = sum(nums)        if ss%4 != 0:            return False         a = ss//4        ll = len(nums)        sumlist = [a]*4        nums.sort(reverse=True)#nums = sorted(nums)[::-1]        def dfs(sumlist,step):            if step == ll and sumlist == [0]*4:                return True             if step == ll or sumlist == [0]*4:                return False            for i in range(4):                if sumlist[i] >= nums[step] :                    sumlist[i] -= nums[step]                    if dfs(sumlist,step + 1):                        return True                    sumlist[i] += nums[step]            return False        return dfs(sumlist,0)
```

