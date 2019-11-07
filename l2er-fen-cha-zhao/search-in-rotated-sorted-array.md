# Search in Rotated Sorted Array

Suppose an array sorted in ascending order is rotated at some pivot unknown to you beforehand.

\(i.e.,`0 1 2 4 5 6 7`might become`4 5 6 7 0 1 2`\).

You are given a target value to search. If found in the array return its index, otherwise return -1.

You may assume no duplicate exists in the array.

分析

先判断m在上半段还是下半段，在每个上半段里，判断target是在m前还是后，m前就是是递增区间，可以直接确定范围，如果是m后，则回到初始问题一样了，继续判断。

```text
class Solution {    public int search(int[] nums, int target) {        if(nums == null || nums.length == 0){            return -1;        }        int s = 0, e = nums.length - 1;        while(s + 1 < e){            int m = s + (e - s)/2;            if(nums[s] < nums[m]){              //m在上半段                //判断target是在m前还是后，m前是递增区间，可以直接确定范围，如果是m后，则和初始问题一样了，继续判断                if(nums[s] <= target && target <= nums[m]){                    e = m;//递增区间                }else{                    s = m;//回到原题                }            }else{                //m在下半段                if(nums[m] <= target && target <= nums[e]){                    s = m;                }else{                    e = m;                }            }        }        if(nums[s] == target){            return s;        }        if(nums[e] == target){            return e;        }            return -1;      }}
```

