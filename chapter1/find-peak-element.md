# Find Peak Element

题目：

There is an integer array which has the following features: The numbers in adjacent positions are different. A\[0\] &lt; A\[1\] && A\[A.length - 2\] &gt; A\[A.length - 1\]. We define a position P is a peek if: A\[P\] &gt; A\[P-1\] && A\[P\] &gt; A\[P+1\] Find a peak element in this array. Return the index of the peak.

分析：

二分让A\[m-1\] &gt; A\[m\]和A\[m\] &lt; A\[m+1\]时候移动，剩下情况A\[m-1\] &lt;A\[m\] &gt;A\[m+1\]就是峰值。

解法：

```text
    public int findPeak(int[] A) {
        // write your code here
        if(A.length == 0)
        return -1;

        int s = 1, e = A.length - 2;//起点和终点位置只会在中间

        while(s + 1 < e){
            int m = s + (e - s)/2;

            if(A[m-1] > A[m]){
                e = m;
            }else if(A[m] < A[m+1]){
                s = m;
            }else{
                e = m; //正好是峰值，移动e好保留s
            }
        }

        if(A[s-1] < A[s] && A[s+1] < A[s])
            return s;

        if(A[e-1] < A[e] && A[e+1] < A[e])
            return e;

            return -1;
    }
```

