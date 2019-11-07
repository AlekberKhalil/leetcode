# Sort Colors

Given an array with_n\_objects colored\_red_,_white\_or\_blue_, sort them so that objects of the same color are adjacent, with the colors in the order red, white and blue.

Here, we will use the integers`0`,`1`, and`2`to represent the color red, white, and blue respectively.

## Notice

You are not suppose to use the library's sort function for this problem.  
You should do it in-place \(sort numbers in the original array\).

**Example**

Given`[1, 0, 1, 2]`, sort it in-place to`[0, 1, 1, 2]`.

分析：

快速排序, partition出一个Index,然后左右各自递归排序

答案;

```text
class Solution {    /**     * @param nums: A list of integer which is 0, 1 or 2      * @return: nothing     */    public void sortColors(int[] nums) {        // write your code here        if(nums == null || nums.length == 0)            return;        qsort(nums, 0, nums.length - 1);    }    public void qsort(int[] nums, int l, int r){        if(l >= r) return;        int index = partition(nums, l, r);        qsort(nums, l, index-1);        qsort(nums, index+1, r);    }    private int partition(int[] nums, int l, int r){        int left = l, right = r;        int pivot = nums[left];        while(left < right){            while(left < right && nums[right] >= pivot){                right --;            }            nums[left] = nums[right];            while(left < right && nums[left] <= pivot){                left ++;            }            nums[right] = nums[left];        }        nums[left] = pivot;        return left;    }}
```

