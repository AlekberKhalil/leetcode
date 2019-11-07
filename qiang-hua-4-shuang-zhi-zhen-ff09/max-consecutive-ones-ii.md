# Max Consecutive Ones II

Given a binary array, find the maximum number of consecutive 1s in this array if you can flip at most one 0.

**Example 1:**

```text
Input: [1,0,1,1,0]Output: 4Explanation: Flip the first zero will get the the maximum number of consecutive 1s.    After flipping, the maximum number of consecutive 1s is 4.
```

**Note:**

* The input array will only contain

  `0`

  and

  `1`

  .

* The length of input array is a positive integer and will not exceed 10,000

**Follow up:**  
What if the input numbers come in one by one as an**infinite stream**? In other words, you can't store all numbers coming from the stream as it's too large to hold in memory. Could you solve it efficiently?

分析

还是Map思想，不过就2个数，直接判断counter了

```text
class Solution:    def findMaxConsecutiveOnes(self, nums: List[int]) -> int:        s,e,counter, ll,maxLen=0,0,0, len(nums),0        while e < ll:            counter = counter if nums[e] == 1 else counter+1            e = e+1            while counter > 1:                counter = counter if nums[s] == 1 else counter-1                s = s+1            maxLen = max(maxLen, e - s)        return maxLen
```

