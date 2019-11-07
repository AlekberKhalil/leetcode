# Kth Largest Element

Find K-th largest element in an array.

## Notice

You can swap elements in the array

**Example**

In array`[9,3,2,4,8]`, the 3rd largest element is`4`.

In array`[1,2,3,4,5]`, the 1st largest element is`5`, 2nd largest element is`4`, 3rd largest element is`3`and etc.

分析：

第k大，增序排列，所以是倒数起，第一大就是最后一个。

可以二分，也可以Minheap，二分可以递归也可以不用helper

[https://yisuang1186.gitbooks.io/-shuatibiji/kth\_largest\_element.html](https://yisuang1186.gitbooks.io/-shuatibiji/kth_largest_element.html)

```text
class Solution {
    /*
     * @param k : description of k
     * @param nums : array of nums
     * @return: description of return
     */
    public int kthLargestElement(int k, int[] nums) {
        // write your code here
        if(nums == null || nums.length == 0 || k > nums.length)
            return -1;
        int n = nums.length;
        return helper(nums, 0, n-1, nums.length - k + 1);
    }

    private int helper(int[] nums, int l, int r, int k){
       if (l == r) {
            return nums[l];
        }
        int index = partition(nums, l, r);
        if(index == k - 1){
                return nums[index];
            }else if(index > k-1){
                return helper(nums, l, index - 1, k);
            }else{
                return helper(nums, index + 1, r, k);
            }

    }

    private int partition(int[] nums, int l, int r){
        int left = l, right = r, pivot = nums[left];
        while(left < right){
            while(left < right && nums[right] >= pivot){
                right --;
            }
            nums[left] = nums[right];
            while(left < right && nums[left] <= pivot){
                left ++;
            }
            nums[right] = nums[left];
        }
        nums[left] = pivot;

        return left;
    }

};
```

