# Find Peak Element

A peak element is an element that is greater than its neighbors.

Given an input array where`num[i] ≠ num[i+1]`, find a peak element and return its index.

The array may contain multiple peaks, in that case return the index to any one of the peaks is fine.

You may imagine that`num[-1] = num[n] = -∞`.

For example, in array`[1, 2, 3, 1]`, 3 is a peak element and your function should return the index number 2.

分析

如果左边可以了nums\[m-1\]&lt;nums\[m\]，就去找右边：start = m。

二分好像是等于的那头，后判断。

```text
class Solution {    public int findPeakElement(int[] nums) {        if(nums == null || nums.length == 0){            return -1;        }        int s = 0, e = nums.length - 1;        int n = nums.length;        while(s + 1 < e){            int m = s + (e - s)/2;            if(nums[m] > nums[m + 1]){                e = m;            }else if(nums[m] > nums[m - 1]){                s = m;            }else{                e = m;            }        }        if(nums[s] > nums[e])            return s;        return e;    }}
```

