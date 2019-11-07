# Maximum Subarray II

题目：

Given an array of integers, find two non-overlapping subarrays which have the largest sum. The number in each subarray should be contiguous.

Return the largest sum.

分析：

首先，很明显的，这题目要求non-overlapping subarray，所以说应该是forward-backward traversal的一个典型应用。在了解maximum subarray的基础上题目应该并不难，只要别写bug就妥帖。

在这里想强调一件事，forward-backward traversal的时候，最后一次求最大值需要思考一下每个vector的含义。一般情况下从0循环到倒数第二个数，并且循环体中用\(forward\[i\] + backward\[i + 1\]\)。只有当做profit的时候，vector的一端为0，才可以循环到底。

**和Best Time to Buy and Sell Stock III 中`left[i] = Math.max(prices[i] - minPrice, left[i-1]);`不一样stock中价格相减，此处数字叠加。**

第二种做法，左数组右移一位，正好和右数组对齐。可以直接相加。

解法：

```text
public int maxTwoSubArrays(ArrayList<Integer> nums) {        // write your code        int minSum =0;        int sum = 0;        int[] left = new int[nums.size()];        int[] right = new int[nums.size()];        int max = Integer.MIN_VALUE;        for(int i = 0; i < nums.size(); i++){            sum += nums.get(i);            max = Math.max(max, sum-minSum);//还是要算前面所有数的最大值，而不是到当前截止（错几次了）            minSum = Math.min(minSum, sum);            left[i] = max;//保留Max给数组赋值        }        minSum = 0;        sum = 0;        max = Integer.MIN_VALUE;        for(int i = nums.size()-1; i >= 0; i--){            sum += nums.get(i);            max = Math.max(max, sum-minSum);            minSum = Math.min(minSum, sum);            right[i] = max;        }        max = Integer.MIN_VALUE;        for(int i = 0; i < nums.size()-1; i++){            max = Math.max(max, left[i] + right[i+1]);//错开以为        }        return max;    }
```

```text
    public int maxTwoSubArrays(ArrayList<Integer> nums) {        // write your code        int localMax =0;        int[] left = new int[nums.size()+1];        int[] right = new int[nums.size()+1];        int n = nums.size();        left[0] = Integer.MIN_VALUE;        //left数组右移一位，正好和right对应了。        for(int i = 0; i < n; i++){            localMax += nums.get(i);            left[i + 1] = Math.max(left[i], localMax);//还是要算前面所有数的最大值，而不是到当前截止（错几次了）            localMax = Math.max(localMax, 0);        }        localMax = 0;        right[n] = Integer.MIN_VALUE;        for(int i = n - 1; i >= 0; i--){            localMax += nums.get(i);            right[i] = Math.max(right[i + 1], localMax);            localMax = Math.max(localMax, 0);        }        int max = Integer.MIN_VALUE;        for(int i = 1; i < n; i++){            max = Math.max(max, left[i] + right[i]);        }        return max;    }
```

