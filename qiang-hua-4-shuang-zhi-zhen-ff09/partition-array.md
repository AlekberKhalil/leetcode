# Partition Array

Given an array`nums`of integers and an int`k`, partition the array \(i.e move the elements in "nums"\) such that:

```text
All elements < k are moved to the left
All elements >= k are moved to the right
```

Return the partitioning index, i.e the first index_i\_nums\[\_i_\] &gt;=_k_.

## Notice

You should do really partition in array\_nums\_instead of just counting the numbers of integers smaller than k.

If all elements in_nums\_are smaller than\_k_, then return_nums.length_

**Example**

If nums =`[3,2,2,1]`and`k=2`, a valid answer is`1`.

分析

对撞型指针,只需要把数移到K左右两边，无需排序，所以没有递归。

答案：

```text
public class Solution {
    /** 
     *@param nums: The integer array you should partition
     *@param k: As description
     *return: The index after partition
     */
    public int partitionArray(int[] nums, int k) {
        //write your code here
        int l=nums.length;
        if(l==0)
        return 0;
        int start=0, end=l-1;

        while(start<=end){
//把>=都换到右边
            while(start<=end && nums[start]<k){
                start++;
            }

           while(start<=end && nums[end]>=k){
                end--;
           }
//把<换到左边                
           if(start<=end){
               int temp=nums[start];
               nums[start]=nums[end];
               nums[end]=temp;

               start++;
                end--;
           }
        }
            return start;
    }
}
```

