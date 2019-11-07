# Maximum Subarray III

Given an array of integers and a number_k_, find k`non-overlapping`subarrays which have the largest sum.

The number in each subarray should be**contiguous**.

Return the largest sum.

**Example**

Given`[-1,4,-2,3,-2,3]`,`k=2`, return`8`

分析：

动归问题。dp\[i\]\[j\]表示从前i个数\( i.e., \[0, i-1\]\) 中取j个subarray得到的最大值，那么要求的结果就是dp\[n\]\[k\]：从前n个数中取k个subarray得到的最大和。

状态转移：从前i个中取j个，那么我们可以从前p个数（i.e., \[0, p-1\]）中取j-1个subarray，再加上从P到i-1这个subarray中的最大和（也就是Maximum Subarray问题）。从这句话里我们也可以读出来p的范围应该是j-1~i-1

d\[i\]\[j\] = max{d\[i\]\[j\],d\[p\]\[j-1\]+maxSubArray\(p+1,i\)}

```text
    public int maxSubArray(int[] nums, int k) {           if(nums ==null || nums.length == 0)                return 0;            int len = nums.length;            //以j结尾的数组里有i个子数组            //f[i][j] = Math.max(f[i][j], f[i-1][m]+ sumFromTo(i-1，j]);            int localMax, max;            int[][] f = new int[k+1][len+1];            int min = nums[0], sum = 0;            for(int i = 1; i <= k; i++){                    for(int j = i; j <= len; j++){                        localMax = 0; max = Integer.MIN_VALUE;                        f[i][j] = Integer.MIN_VALUE;                        for(int m = j-1; m >= i-1; m--){//i->j之间最大的subarray sum,需要从后往前算，这样求的是后端固定的maxSum                            //从后往前，因为我们只需要从j-1到i-1内最大的，前面开始的话包括了i-1之前的值。和back-forward概念一样                            //locaMax一定以当年Nums[m]结尾的sum，但是max不一定以当前结尾，而是截止到m为止最大，可有该nums[m]可无                              localMax = Math.max(nums[m], localMax + nums[m]);                             max = Math.max(localMax, max);                             f[i][j] = Math.max(f[i][j], f[i-1][m]+ max);                        }                }               }            return f[k][len];    }
```

分析：

local\[i\]\[k\]表示前i个元素取k个子数组并且必须包含第i个元素的最大和。

global\[i\]\[k\]表示前i个元素取k个子数组不一定包含第i个元素的最大和。

local\[i\]\[k\]的状态函数：

```text
max(global[i-1][k-1], local[i-1][k]) + nums[i-1]
```

local有两种情况，第一种是第i个元素自己组成一个子数组，则要在前i－1个元素中找k－1个子数组，第二种情况是第i个元素属于前一个元素的子数组，因此要在i－1个元素中找k个子数组（并且必须包含第i－1个元素，这样第i个元素才能合并到最后一个子数组中），取两种情况里面大的那个。

global\[i\]\[k\]的状态函数：

```text
max(global[i-1][k]，local[i][k])
```

glocal有两种情况，第一种是不包含第i个元素，所以要在前i－1个元素中找k个子数组，第二种情况为包含第i个元素，在i个元素中找k个子数组且必须包含第i个元素，取两种情况里面大的那个

```text
    public int maxSubArray(int[] nums, int k) {        int n = nums.length;        // if(n < 1){        //     return 0;        // }//local[i][k]表示前i个元素取k个子数组并且必须包含第i个元素的最大和。//global[i][k]表示前i个元素取k个子数组不一定包含第i个元素的最大和。        int[][] local = new int[n + 1][k + 1];        int[][] global = new int[n + 1][k + 1];        for(int j = 1; j <= k; j ++){            for(int i = j; i <= n; i ++){                local[j - 1][j] = Integer.MIN_VALUE;//小于 i 的数组不能够partition,取最小防止被取到。                //1.要不i自成一组，不跟前面，所以用global因为前面i-1是否包含都行                //2.要不i跟前面成一组，则i-1必须包含，因为是连续的，所以用local                local[i][j] = Math.max(global[i-1][j-1], local[i-1][j]) + nums[i - 1];                if(i == j){                    global[i][j] = local[i][j];                }else{                //1.不取i，所以前面i-1包不包都可以，用global                //2.取i,必须包含i,所以用local                    global[i][j] = Math.max(global[i - 1][j], local[i][j]);                }            }        }        return global[n][k];    }
```

