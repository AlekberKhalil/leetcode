# Partition Array by Odd and Even

Partition an integers array into odd number first and even number second.

**Example**

Given`[1, 2, 3, 4]`, return`[1, 3, 2, 4]`

分析

对撞指针，quick select，不必递归

答案

```text
public class Solution {    /**     * @param nums: an array of integers     * @return: nothing     */    public void partitionArray(int[] nums) {        // write your code here;        if(nums == null || nums.length == 0)            return;        int left = 0, right = nums.length - 1, pivot = nums[left];        while(left < right){            while(left < right && nums[right] % 2 == 0){                right --;            }            nums[left] = nums[right];            while(left < right && nums[left] % 2 == 1){                left ++;            }            nums[right] = nums[left];        }        nums[left] = pivot;    }}
```

