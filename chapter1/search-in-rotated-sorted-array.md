# Search in Rotated Sorted Array

题目：

Suppose a sorted array is rotated at some pivot unknown to you beforehand.

\(i.e., 0 1 2 4 5 6 7 might become 4 5 6 7 0 1 2\).

You are given a target value to search. If found in the array return its index, otherwise return -1.

You may assume no duplicate exists in the array.

Example

For \[4, 5, 1, 2, 3\] and target=1, return 2.

For \[4, 5, 1, 2, 3\] and target=0, return -1.

分析：

判断Mid处于上半段还是下半段后，在单调递增/递减区间内可以判断，否则丢回去继续while

解法：

```text
public int search(int[] A, int target) {        // write your code here        if(A.length == 0)        return -1;        int s = 0, e = A.length - 1;        while(s + 1 < e){            int m = s + (e - s)/2;            if (A[m] == target) {                return m;            }             if(A[m] > A[s]){//m在上半段                if(A[s] <= target && target <= A[m]){//在单调递增区间才能判定，否则还是2条断线，丢回去继续while                    e = m;                }else{                    s = m;                }            }            else{                if(A[m] <= target && target <= A[e]){                    s = m;                }else{                    e = m;                }            }        }        if(A[s] == target)            return s;        if(A[e] == target)            return e;            return -1;    }
```

