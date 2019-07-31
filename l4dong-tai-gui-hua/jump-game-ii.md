# Jump Game II

Given an array of non-negative integers, you are initially positioned at the first index of the array.

Each element in the array represents your maximum jump length at that position.

Your goal is to reach the last index in the minimum number of jumps.

For example:  
Given array A =`[2,3,1,1,4]`

The minimum number of jumps to reach the last index is`2`. \(Jump`1`step from index 0 to 1, then`3`steps to the last index.\)

**Note:**  
You can assume that you can always reach the last index.

分析

还是贪心法，一直纪录最大的，loop i到了当前last,每次last设置为最大

```text
class Solution {
    public int jump(int[] nums) {
        int n = nums.length, step = 0, last = 0, max = 0;
        for(int i = 0; i < n - 1, i ++){//只到n-1 到最后一步不要step++了
            max = Math.max(max, i + nums[i]);
            if(i == last){
                last = max;
                step ++;
            }

        }
        return step;
    }
}
```

