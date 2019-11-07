# Maximum Product Subarray

Given an integer array `nums`, find the contiguous subarray within an array \(containing at least one number\) which has the largest product.

**Example 1:**

```text
Input: [2,3,-2,4]Output:6Explanation: [2,3] has the largest product = 6.
```

**Example 2:**

```text
Input: [-2,0,-1]Output: 0Explanation: The result cannot be 2, because [-2,-1] is not a subarray.
```

分析

2个负数相乘可以得到最大值，需要存储当前最小的数。

```text
*  second method: DP: curMax is the max of product contains the current element; *        since element can be negetive, maximum value can be obtain by product of two negtive numbers; *        we also need to store the current minimum product; *        when go to next element; *        if nums[i] < 0; curMax = Math.max(nums[i], nums[i]* curMin); *                        curMin = Math.min(nums[i], nums[i]* curMax); *                        (can swap curMax and curMin, and conbine the expression for those two conditions. *        else:           curMax = Math.max(nums[i], nums[i]* curMax); *                        curMin = Math.min(nums[i], nums[i]* curMin);
```

可以直接交换curMin和curMax

答案

```text
public class Solution {    /**     * @param nums: An array of integers     * @return: An integer     */    public int maxProduct(int[] nums) {        // write your code here        if(nums == null || nums.length == 0) {            return 0;        }        int n = nums.length;        int max = nums[0], curMin = nums[0], curMax = nums[0];        for(int i = 1; i < n; i ++){            if(nums[i] < 0) {            int temp = curMax;               curMax = curMin;               curMin = temp;            }             curMax = Math.max(curMax * nums[i], nums[i]);            curMin = Math.min(curMin * nums[i], nums[i]);            max = Math.max(max, curMax);        }        return max;    }}
```

python

负负得正，所以2个数组，一个存最大一个存最小

```text
class Solution:    def maxProduct(self, nums: List[int]) -> int:        n = len(nums)        dp = [1] + [i for i in nums]        mdp = [1] + [i for i in nums]        res = float('-inf')        for i in range(1,n+1):            dp[i] = max(dp[i],dp[i-1]*nums[i-1],mdp[i-1]*nums[i-1])            mdp[i] = min(mdp[i],mdp[i-1]*nums[i-1],dp[i-1]*nums[i-1])            res = max(res,dp[i])        return res
```

因为只和前面状态min,max相关，并且当前态就能比较出res，只要设置这3个变量即可

```text
class Solution:    def maxProduct(self, nums: List[int]) -> int:                mn,mx,res = 1,1,float('-inf')        for i in nums:            mn,mx = min(i, mn*i,mx*i),max(i,mx*i,mn*i)            res = max(mn,mx,res)        return res
```

