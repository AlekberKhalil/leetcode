# 2 Sum

题目：

Given an array of integers, find two numbers such that they add up to a specific target number.

The function twoSum should return indices of the two numbers such that they add up to the target, where index1 must be less than index2. Please note that your returned answers \(both index1 and index2\) are NOT zero-based.

分析：

两指针时间不行，错了两处，一map里存num\[i\]和i。第二key是num\[i\]不是target-num\[i\]，返回的是Index.

要返回下标 只能用Hash.如果要找多对组合的话 ，把==target的那对删一个数，然后继续。

解答：

```text
    public int[] twoSum(int[] nums, int target) {
        int[] ret = new int[2];
        // if(nums == null || nums.length == 0)
        //     return ret;
        HashMap<Integer, Integer> sumMap = new HashMap<Integer, Integer>();
        for(int i = 0; i < nums.length; i++){
            if(sumMap.containsKey(target - nums[i])){
                ret[0] = i;
                ret[1] = sumMap.get(target - nums[i]);
            }else{
                sumMap.put(nums[i], i);
            }
        }
        return ret;
    }
```

