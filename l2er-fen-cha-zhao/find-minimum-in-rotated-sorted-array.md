# Find Minimum in Rotated Sorted Array

Suppose an array sorted in ascending order is rotated at some pivot unknown to you beforehand.

\(i.e.,`0 1 2 4 5 6 7`might become`4 5 6 7 0 1 2`\).

Find the minimum element.

You may assume no duplicate exists in the array.

分析

最后一个词作为target,然后找第一个&lt;=target的数字

```text
class Solution {    public int findMin(int[] nums) {        if(nums == null || nums.length == 0){            return -1;        }        int s = 0, e = nums.length - 1, target = nums[nums.length - 1];        while(s + 1 < e){            int m = s + (e - s)/2;            //first <= target            if(nums[m] <= target){                e = m;            }else{                s = m;            }                   }        if(nums[s] <= target)            return nums[s];        else            return nums[e];    }}
```

