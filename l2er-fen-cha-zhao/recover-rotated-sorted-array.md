# Recover Rotated Sorted Array

Given a**rotated**sorted array, recover it to sorted array in-place.

**Clarification**

What is rotated array?

* For example, the orginal array is \[1,2,3,4\], The rotated array of it can be \[1,2,3,4\], \[2,3,4,1\], \[3,4,1,2\], \[4,1,2,3\]

**Example**

`[4, 5, 1, 2, 3]`-&gt;`[1, 2, 3, 4, 5]`

分析

找出转折位置，三步翻转，先每段，再整体

不知道为什么二分找转折点不行。

```text
public class Solution {    /*     * @param nums: An integer     * @return:      */    public void recoverRotatedSortedArray(List<Integer> nums) {        // write your code here        if(nums == null || nums.size() == 0){            return ;        }        // int s = 0, e = nums.size() - 1, n = nums.size();        // int target = nums.get(n - 1);        // while(s + 1 < e){        //     int m = s + (e - s)/2;        //     if(nums.get(m) > target){        //         s = m;        //     }else{        //         e = m;        //     }        // }        // int index  = nums.get(s) <= target ? s : e;        int n = nums.size();        for(int i = 0; i < n - 1; i++){            if(nums.get(i + 1) < nums.get(i)){                reverse(nums, 0, i);                 reverse(nums, i + 1, n - 1);                 reverse(nums, 0, n - 1);                 return;            }        }    //     int pos = -1;    //     for(int i = 0; i < nums.size()-1; i++){    //         if(nums.get(i) > nums.get(i+1)){    //             pos = i;    //             break;    //         }    //     }    //     reverse(nums, 0, pos);    //     reverse(nums, pos+1, nums.size()-1);    //     reverse(nums, 0, nums.size()-1);    // }    // public void reverse(List<Integer> nums, int start, int end){    //     while(start < end){    //         int temp = nums.get(start);    //         nums.set(start++, nums.get(end));    //         nums.set(end--, temp);    //     }    }    private void reverse(List<Integer> nums, int start, int end){        int s = start, e = end;        while(s < e){            int temp = nums.get(s);            nums.set(s, nums.get(e));            nums.set(e, temp);             s ++;            e --;        }    }};
```

