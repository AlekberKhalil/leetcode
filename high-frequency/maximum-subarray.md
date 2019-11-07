# Maximum Subarray

题目：

Given an array of integers, find a contiguous subarray which has the largest sum.

分析：

一样的题目：Best time to buy and sell stock

凡是和subarray子数组相关的问题，都要想到子数组和是俩前缀和相减（惯用套路）nums\[i...j\] = sum\[j\]-sum\[i-1\]

最后强调一点，这道题目强调顺序，应该先做maxSum，后做minSum，这也保证了当数组只有一个元素的时候，依然符合规律。

前缀和做法，和LocalMax

[http://blog.hyoung.me/cn/2017/02/maximum-subarray/](http://blog.hyoung.me/cn/2017/02/maximum-subarray/)

解法：

```text
public int maxSubArray(int[] nums) {        // write your code        int minSum =0, ret = Integer.MIN_VALUE;        int sum = 0;        for(int i = 0; i < nums.length; i++){            sum += nums[i];            ret = Math.max(ret, sum-minSum);            minSum = Math.min(minSum, sum);//这里保存min可以省一个loop        }        return ret;    }
```

```text
    public int maxSubArray(int[] nums) {        // write your code        int localMax =0, globalMax = Integer.MIN_VALUE;        for(int i = 0; i < nums.length; i++){            localMax += nums[i];            globalMax = Math.max(globalMax, localMax);            localMax = Math.max(localMax, 0);        }        return globalMax;    }
```

