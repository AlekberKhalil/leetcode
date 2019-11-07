# Product of Array Except Self

Given an array ofnintegers wheren&gt; 1,`nums`, return an array`output`such that`output[i]`is equal to the product of all the elements of`nums`except`nums[i]`.

Solve it**without division**and in O\(n\).

For example, given`[1,2,3,4]`, return`[24,12,8,6]`.

**Follow up:**  
Could you solve it with constant space complexity? \(Note: The output array**does not**count as extra space for the purpose of space complexity analysis.\)

分析

3遍loop, left, right数组叠加乘，不含当前nums\[i\]。然后ret\[i\]用left\[i\]\*right\[i\]。

```text
class Solution {    public int[] productExceptSelf(int[] nums) {                if(nums == null && nums.length == 0){            return null;        }        int n = nums.length;        int[] ret = new int[n];        int[] left = new int[n];        int[] right = new int[n];        for(int i = 0; i < n; i ++){            if(i == 0){                left[i] = 1;            }else{                left[i] = left[i - 1] * nums[i - 1];            }                   }        for(int i = n - 1; i >= 0; i --){            if(i == n - 1){                right[i] = 1;            }else{                right[i] = right[i + 1] * nums[i + 1];            }                   }        for(int i = 0; i < n; i ++){            ret[i] = left[i] * right[i];        }         return ret;    }}
```

constant space complexity,用ret数组直接替代左右数组

```text
class Solution {    public int[] productExceptSelf(int[] nums) {                if(nums == null && nums.length == 0){            return null;        }        int n = nums.length;        int[] ret = new int[n];        int temp = 1;        for(int i = 0; i < n; i ++){            if(i == 0){                ret[i] = 1;            }else{                ret[i] = ret[i - 1] * nums[i - 1];            }                   }        for(int i = n - 2; i >= 0; i --){            temp = temp * nuams[i + 1];            ret[i] = ret[i] * temp;                   }        return ret;    }}
```

