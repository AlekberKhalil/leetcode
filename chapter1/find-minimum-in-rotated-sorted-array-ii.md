# Find Minimum in Rotated Sorted Array II

题目：

Suppose a sorted array is rotated at some pivot unknown to you beforehand.

\(i.e., 0 1 2 4 5 6 7 might become 4 5 6 7 0 1 2\).

Find the minimum element.

The array may contain duplicates.

分析：

在I的基础上，相等时候末尾end--

解法：

```text
    public int findMin(int[] num) {
        // write your code here
        if(num.length == 0)
        return -1;

    int s = 0, e = num.length - 1;
    int target = num[e];

    while(s + 1 < e){
        int m = s + (e - s)/2;
        if(num[m] == num[e]){
            e--;
        }else if(num[m] < target){
            e = m;
        }else{
            s = m;
        }
    }

    if(num[s] < target)//不是<=
        return num[s];

    return num[e];
    //return Math.min(num[s], num[e]);也行
    }
```

