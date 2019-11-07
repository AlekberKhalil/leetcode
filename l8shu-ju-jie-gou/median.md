# Median

Given a unsorted array with integers, find the median of it.

A median is the middle number of the array after it is sorted.

If there are even numbers in the array, return the`N/2`-th number after sorted.

**Example**

Given`[4, 5, 1, 2, 3]`, return`3`.

Given`[7, 9, 4, 5]`, return`5`.

分析

快速排序，选最左的数为Pivot，则先从右边开始。while里l,r互换，最后l是答案

次数size是一半，因为start, end ,l都是根据原数组大小的，没变过，所以size也不变。

```text
public class Solution {    /*     * @param nums: A list of integers     * @return: An integer denotes the middle number of the array     */    public int median(int[] nums) {        // write your code here        int n = nums.length;        //根据题意，偶数用n/2，所以不论奇偶，都可以用(n + 1) / 2表示中位数        return helper(nums, 0, n - 1, (n + 1) / 2);    }    int helper(int[] nums, int s, int e, int size){        int pivot = nums[s];        int l = s, r = e;        while(l < r){            while(pivot <= nums[r] && l < r){                r --;            }            nums[l] = nums[r];            while(pivot >= nums[l] && l < r){                l ++;            }            nums[r] = nums[l];        }        nums[l] = pivot;        //因为start, end ,l都是根据原数组大小的，没变过，所以size也不变。        if(l + 1 < size){            return helper(nums, l + 1, e, size);        }else if(l + 1 > size){            return helper(nums, s, l - 1, size);        }else{            return nums[l];        }    }}
```

