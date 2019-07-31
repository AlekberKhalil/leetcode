# Single Number

题目：

Given 2\*n + 1 numbers, every numbers occurs twice except one, find it.

分析：

异或，相同数异或会抵消,两两抵消。a^a=0 0^a = a

解法：

```text
 public int singleNumber(int[] A) {
        // Write your code here
        int ret = 0;
        for(int i = 0; i< A.length; i++){
            ret^=A[i];
        }
        return ret;
    }
```

