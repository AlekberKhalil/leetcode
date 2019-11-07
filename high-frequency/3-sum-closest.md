# 3 Sum Closest

题目：

Given an array S of n integers, find three integers in S such that the sum is closest to a given number, target. Return the sum of the three integers.

You may assume that each input would have exactly one solution.

分析：

双指针，不断更新最小diff.不知道为什么不去重。

解法：

```text
    public int threeSumClosest(int[] nums, int target) {        int sum = 0, minDiff = Integer.MAX_VALUE;        Arrays.sort(nums);        for(int j = 0; j < nums.length - 2; j++){                int first = nums[j], start = j + 1, end = nums.length - 1;                            while(start < end){                    int second = nums[start], third = nums[end];                    int localSum = first + second + third;                    int diff = Math.abs(target - localSum);                    if(diff < minDiff){                        sum = localSum;                        minDiff = diff;                    }                    if(localSum < target){                        start ++;                                           }else{                        end --;                    }                                               }        }        return sum;            }
```

