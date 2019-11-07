# Binary Search and Sorted Array

二分法

1. 给有序整数组nums，找出_**any/first/last position of target**_ in nums，通常找临界点。
2. 用logn而非n，从复杂度想到算法
3. 取中间数，比较大小，决定在左或者在右。复杂度 logn
4. while\(start+1&lt;end\) 出来时相邻或者相交start+1=end 相邻。 start+1&gt;end 相交。都当做相邻处理？相邻退出不会导致死循环
5. mid=start+\(end-start\)/2 即使Integer很大也不会溢出
6. 直接等于mid
7. 判断start end target 关系

binary search 模板

```text
//first occurrence of targetint binarySearch(vector<int> &A, int target){    if(A.size()==0){        return -1;    }    int start=0;    int end=A.size()-1;    int mid;    while(start+1<end){        mid=start+（end-start）/2;        if(A[mid]==target)            end=mid;        else if(A[mid]>target)            end=mid; //不用mid+1之类        else            start=mid;    }//Mid不变，所以最后需要分别判断    if(A[start]==target)        return start;    if(A[end]==target)        return end;    return -1;}
```

二分查找range

range先找左bound，每次移动end，找右Bound，\(可能因为左边的肯定都比左边界小，所以移动右边，右边界同理\)每次移动start,中间要reset start和end

二分查找matrix

从左下或者右上。这样每次都可以排除一行或者一列。普通正向或者反向都不好用

```text
start =0, end = row * column -1;int number = matrix[mid / column][mid % column]; //都是用column
```

三步翻转法

三步翻转法可以实现rotated和rotate数组还原

