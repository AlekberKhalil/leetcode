# Merge Sorted Array

Given two sorted integer arraysnums1andnums2, mergenums2intonums1as one sorted array.

**Note:**  
You may assume thatnums1has enough space \(size that is greater or equal tom+n\) to hold additional elements fromnums2. The number of elements initialized innums1andnums2aremandnrespectively.

分析

小数组归并到大数组，用大的数组从后往前填充。到最后只需要检查小数组是否还有余值，若有则加入。

```text
class Solution {
    public void merge(int[] nums1, int m, int[] nums2, int n) {
        int i = m - 1, j = n - 1, k = m + n - 1;
        while(j >= 0 && i >= 0){
                nums1[k --] = nums1[i] > nums2[j] ? nums1[i --] : nums2[j --];            
        }
        while(j >= 0){
            nums1[k --] = nums2[j --];
        }        
        }        
}
```

