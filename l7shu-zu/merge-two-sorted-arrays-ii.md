# Merge Two Sorted Arrays II

Merge two given sorted integer array\_A\_and\_B\_into a new sorted integer array.

**Example**

A=`[1,2,3,4]`

B=`[2,4,5,6]`

return`[1,2,2,3,4,4,5,6]`

分析

第三个数组正序存放

```text
public class Solution {    /*     * @param A: sorted integer array A     * @param B: sorted integer array B     * @return: A new sorted integer array     */    public int[] mergeSortedArray(int[] A, int[] B) {        // write your code here        int m = A.length, n = B.length;        int[] c = new int[m + n];        int i = 0,j = 0, k = 0;        while(i < m && j < n){            c[k ++] = A[i] < B[j] ? A[i ++] : B[j ++];        }        if(i < m){            while(i < m)            c[k ++] = A[i ++];        }else if(j < n){            while(j < n)            c[k ++] = B[j ++];        }        return c;    }}
```

