# Single NumberII

题目：

Given 3\*n + 1 numbers, every numbers occurs triple times except one, find it.

分析：

3个数抵消，不进位加法，变成三进制，每位单独加起来，得到的数就是结果

A\[j\] &gt;&gt; i & 1; 用来把一个整数拆成Bit位

解法：

```text
public int singleNumberII(int[] A) {
        // write your code here
        int[] bit = new int[32];
        int ret = 0;
        for(int i = 0; i < 32; i++){
            for(int j = 0; j < A.length; j++){
               bit[i] +=  A[j] >> i & 1; //用来把一个整数拆成Bit位
               bit[i] %= 3;//三进制
            }
            ret |= bit[i] << i;
        }
        return ret;
    }
```

