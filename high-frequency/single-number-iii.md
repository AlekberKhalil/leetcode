# Single Number III

题目：

Given 2\*n + 2 numbers, every numbers occurs twice except two, find them.

分析：

把2n+2变成2n+1问题,把原来集合分为2个集合。\(c-1\)&c 去掉最后一个1的作用，c-\(c-1\)&c得到最后1

解法：

```text
public List<Integer> singleNumberIII(int[] A) {        // write your code here        int xor = 0;        for(int i = 0; i < A.length; i++){            xor ^= A[i];        }        int lastBit = xor - (xor & (xor - 1));        int group1 = 0, group2 = 0;        for(int i = 0; i < A.length; i++){            if((A[i] & lastBit) == 0){                group1 ^= A[i];            }else{                group2 ^= A[i];            }        }        List<Integer> ret =  new ArrayList<Integer>();        ret.add(group1);        ret.add(group2);        return ret;    }
```

