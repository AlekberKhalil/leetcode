# Subarray Sum II

## Question <a id="question"></a>

Given an integer array, find a subarray where the sum of numbers is in a given interval. Your code should return the number of possible answers. \(The element in the array should be positive\)

Example

Given \[1,2,3,4\] and interval = \[1,3\], return 4. The possible answers are:

\[0, 0\] \[0, 1\] \[1, 1\] \[2, 2\]

## Solution <a id="solution"></a>

[http://blog.hyoung.me/cn/2017/02/subarray-sum-ii/](http://blog.hyoung.me/cn/2017/02/subarray-sum-ii/)

1.二分法，等于固定尾部寻头。presum先做

分别为第一个大于或等于prefixSum\[i\] - high的位置，即最左边的位置，以及最后一个小于或等于prefixSum\[i\] - low的位置，即最右边的位置。 看上去这是两种二分搜索，但这里有个小技巧，那就是把后一个条件稍稍修改，变成第一个大于或等于prefixSum\[i\] - low + 1的位置，等效于我们把需要找的位置往后移了一位。

```text
子数组和落在区间里
pre[i]-3<=pre[j]<=pre[i]-1
```

2.双窗口滑动，等于固定头部寻尾。维护2个滑动窗口一个窗口代表目标区间的最小值，另一个则是目标区间的最大值。相较于常规一个指针维护滑动窗口尾部，这里用两个尾指针分别维护这两个滑动窗口。最大值尾指针始终大于最小值尾指针。

[http://massivealgorithms.blogspot.com/2017/05/lintcode-138-404-subarray-sum-iii.html](http://massivealgorithms.blogspot.com/2017/05/lintcode-138-404-subarray-sum-iii.html)

不懂为什么highbound - lowbound

答案

二分

```text
public int subarraySumII(int[] A, int start, int end) {
        int[] sum = new int[A.length + 1];
        int count = 0;
        for(int i = 1; i <= A.length; i++){
            sum[i] = sum[i-1] + A[i-1];
        }
        for(int i = 1; i <= A.length; i++){
            //固定尾端为i，传入数组长度为I,所以要有I做参数，和window相比,window固定头
            int lowBound = find(A, i, sum[i] - end);
            int highBound = find(A, i, sum[i] - start + 1);
            count += highBound - lowBound;
        }
        return count;

    }
    //target <= j
    private int find(int[] A, int len, int target){
        if(A[len -1] < target)
            return len;
        int start = 0, end = len - 1, first = 0;
        while(start + 1 < end){
            int mid = start + (end - start)/2;
            if(A[mid] >= target){
                //first = mid;
                end = mid;
            }else {
                start = mid;
            }
        }
        if(A[start] >= target){
            return start;
        }
        if(A[end] >= target){
            return end;
        }
        return end;
    }
```

双移动窗口

```text
    public int subarraySumII(int[] A, int start, int end) {
        int head = 0, ft = 0, st = 0, n = A.length, sf = 0, ss = 0, count = 0;

        for(int i = 0; i < n; i++){
            while(ft < n && sf + A[ft] < start){
                ft ++;
                sf += A[ft];
            }
            //第二指针不能低于第一指针
            if(st < ft){
                st = ft;
                ss = sf;
            }

            while(st < n && ss + A[st] <= end){
                st ++;
                ss += A[st];
            }

            count += (st - ft);
            sf -= A[i];
            ss -= A[i];
        }
        return count;

    }
```

