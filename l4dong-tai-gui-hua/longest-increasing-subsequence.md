# Longest Increasing Subsequence（FB 区间DP）

Given an unsorted array of integers, find the length of longest increasing subsequence.

For example,  
Given`[10, 9, 2, 5, 3, 7, 101, 18]`,  
The longest increasing subsequence is`[2, 3, 7, 101]`, therefore the length is`4`. Note that there may be more than one LIS combination, it is only necessary for you to return the length.

Your algorithm should run in O\(n2\) complexity.

**Follow up:**Could you improve it to O\(nlogn\) time complexity?

分析

f\(i\)代表前I个数最长LIS，并且以I结尾

一个sequence 双重循环 第一循环i 第二循环j 从0到i,true之后要break

```text
class Solution {    public int lengthOfLIS(int[] nums) {        if(nums == null || nums.length == 0)            return 0;        int[] f = new int[nums.length];        int max = 0;        for(int  i = 0; i < nums.length; i ++){            f[i] = 1;//最坏情况只有当前这个元素，所以1            for(int  j = 0; j < i; j ++){//需要这层循环，因为对于每个nums[i]来说，前面情况都不一样，需要重新从头loop判断                if(nums[j] < nums[i]){                    f[i] = f[i] > f[j] + 1 ? f[i] : f[j] + 1;//当前f[i]可能已经比当前f[j]+1更大                }                             }             max = Math.max(f[i], max);        }        return max;    }}
```

python dp

```text
class Solution:    def lengthOfLIS(self, nums):        """        :type nums: List[int]        :rtype: int        """        if not nums:            return 0        n = len(nums)        f=[0]*n        res = 0        for i in range(n):            f[i]=1            for j in range(i):                #nums[j]<nums[i]，当前f[j]的序列len可++                if nums[j]<nums[i] and f[j]+1>f[i]:#一定记得f[j]+1>f[i]                    f[i] = f[j]+1            res = max(res,f[i]) #忘了这个        return res
```

iterarive

Arrays.binarySearch返回第一个大于key的数的Index，所以Key_代替_了第一个比它大的数。开始时候dp是空的。

```text
class Solution {    public int lengthOfLIS(int[] nums) {        int[] arr = new int[nums.length];        int len = 0;        for(int n : nums){           int pos = Arrays.binarySearch(arr, 0, len, n);            if(pos < 0){                pos = -(pos + 1);             }           arr[pos] = n;        if(pos == len) len ++;     //无法通过dp有效长度得到，因为dp开始长度就确定了，所以一旦填充就增加Len。               }        return len;    }}
```

python 用bisect\_left返回的是该插入的位置

```text
import bisectclass Solution:    def lengthOfLIS(self, nums):        """        :type nums: List[int]        :rtype: int        """        ret=[]        for i in nums:            index = bisect.bisect_left(ret,i)            if index==len(ret):                ret.append(i)            else:                ret[index] = i        return len(ret)
```

