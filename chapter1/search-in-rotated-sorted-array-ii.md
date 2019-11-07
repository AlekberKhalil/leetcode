# Search in Rotated Sorted Array II

题目：

Follow up for "Search in Rotated Sorted Array": What if duplicates are allowed?

Would this affect the run-time complexity? How and why?

Write a function to determine if a given target is in the array.

分析：

复杂度是肯定要变差的，如果所有元素都是1，就一个是2，然后找2，二分法的特性就被破坏了，所以worst case变成linear的了。

解法：

```text
 只需要举出能够最坏情况的数据是 [1,1,1,1... 1] 里有一个0即可。 在这种情况下是无法使用二分法的，复杂度是O(n)
 因此写个for循环最坏也是O(n)，那就写个for循环就好了
```

```text
二分法

public boolean search(int[] A, int target) {
        if(A.length == 0)
        return false;

        int s = 0, e = A.length - 1;

        while(s + 1 < e){
            int m = s + (e - s)/2;
            if (A[m] == target) {
                return true;
            } 
            if(A[m] == A[s]){
                s++;
                continue;
            }
            else if(A[m] > A[s]){//m在上半段
                if(A[s] < target && target < A[m]){//在单调递增区间才能判定，否则还是2条断线，丢回去继续while
                    e = m;
                }else{
                    s = m;
                }
            }else if(A[m] == A[e]){
                e--;
                continue;
            }
            else{
                if(A[m] < target && target < A[e]){
                    s = m;
                }else{
                    e = m;
                }
            }
        }

        if(A[s] == target || A[e] == target)
            return true;

            return false;
    }
```

直接for loop

```text
  public boolean search(int[] A, int target) {
        for (int i = 0; i < A.length; i ++) {
            if (A[i] == target) {
                return true;
            }
        }
        return false;
    }
```

