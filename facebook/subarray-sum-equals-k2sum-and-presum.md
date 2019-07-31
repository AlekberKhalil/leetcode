# Subarray Sum Equals K（2sum and presum）

Given an array of integers and an integer**k**, you need to find the total number of continuous subarrays whose sum equals to**k**.

**Example 1:**

```text
Input:
nums = [1,1,1], k = 2

Output:
 2
```

**Note:**

1. The length of the array is in range \[1, 20,000\].
2. The range of numbers in the array is \[-1000, 1000\] and the range of the integer **k** is \[-1e7, 1e7\].

分析：

```text
PrefixSum + Dictionary
> Time Complexity O(N)
> Space Complexity O(N)
```

这里没有presum数组，只有sum累积

这里map存个数 map\[sum\]=count

对map和ret都是+=1不是=！！！！！

PYTHON MAP:MAP.GET\(KEY,0\)

```text
 if we know SUM[0, i - 1] and SUM[0, j], then we can easily get SUM[i, j]. 因为不包含前数，所以Map[0]=1
```

```text
import collections

class Solution:
    def subarraySum(self, nums, k):
        """
        :type nums: List[int]
        :type k: int
        :rtype: int
        """
        if not nums:
            return 0
        ret = 0
        n = len(nums)

        map = collections.defaultdict(int)
        map[0] = 1 #因为前面总是不包含，所以需要map[0]补足？
        sum=0
        for i in range(n):
            sum+=nums[i]
            if sum - k in map:
                ret += map[sum- k]#+= 不是 =
            map[sum] += 1 #+= 不是 =
        return ret
```

