# Minimum Size Subarray Sum

Given an array of**n**positive integers and a positive integer**s**, find the minimal length of a**contiguous**subarray of which the sum ≥**s**. If there isn't one, return 0 instead.

For example, given the array`[2,3,1,2,4,3]`and`s = 7`,  
the subarray`[4,3]`has the minimal length under the problem constraint.

分析

窗口类指针。for i loop里直接跟上while j 的条件，i,j无需错开，开始直接相等。

```text
class Solution {
    public int minSubArrayLen(int s, int[] nums) {
        if(nums == null || nums.length == 0)
            return 0;
        int cnt = Integer.MAX_VALUE, n = nums.length, sum = 0;
        for(int i = 0, j = 0; i < n; i ++){
            //直接while开始，不需要i,j开始错开。
            while(j < n && sum < s){               
                sum += nums[j ++];                            
            }
            //while里俩条件，不保证sum存在，所以此处需要再判断。
            if(s <= sum){
                cnt = Math.min(j - i, cnt);
            }            
            sum -= nums[i];
        }
        if(cnt == Integer.MAX_VALUE){
            return 0;
        }
        return cnt;
    }
}
```

python

