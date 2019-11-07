# Search Insert Position

Given a sorted array and a target value, return the index if the target is found. If not, return the index where it would be if it were inserted in order.

You may assume no duplicates in the array.

Here are few examples.  
`[1,3,5,6]`, 5 → 2  
`[1,3,5,6]`, 2 → 1  
`[1,3,5,6]`, 7 → 4  
`[1,3,5,6]`, 0 → 0

分析

二分，主要是最后对s,e的判断，分为&lt;= s, &gt; e 和 s, e 之间。

答案

```text
class Solution {    public int searchInsert(int[] nums, int target) {       if(nums == null || nums.length == 0){            return 0;        }        int s = 0, e = nums.length - 1;        while(s + 1 < e){            int m = s + (e - s)/2;            if(nums[m] == target){                return m;            }else if(nums[m] < target){                s = m;            }else{                e = m;            }        }        if(nums[s] >= target){            return s;        }        if(nums[e] < target){            return e + 1;        }        return e;    }}
```

