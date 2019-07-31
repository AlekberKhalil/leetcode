# Wiggle Sort II

Given an unsorted array`nums`, reorder it such that

```text
nums[0] < nums[1] > nums[2] < nums[3]....
```

## Notice

You may assume all input has valid answer.

**Example**

Given`nums = [1, 5, 1, 1, 6, 4]`, one possible answer is`[1, 4, 1, 5, 1, 6]`.

Given`nums = [1, 3, 2, 2, 3, 1]`, one possible answer is`[2, 3, 1, 3, 1, 2]`.

分析

除了sort，可以用partition找出中位数，奇数位用从end起的数 fill,偶数位用从mid起的数fill

答案

```text
class Solution {
public:
    /**
     * @param nums a list of integer
     * @return void
     */  
    void wiggleSort(vector<int>& nums) {
        // Write your code here
        vector<int> tmp = nums;
        int n = nums.size(), k = (n + 1) / 2, j = n; 
        sort(tmp.begin(), tmp.end());
        for (int i = 0; i < n; ++i) {
            nums[i] = i & 1 ? tmp[--j] : tmp[--k];
        }
    }
};
```

