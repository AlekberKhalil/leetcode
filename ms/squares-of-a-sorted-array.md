# Squares of a Sorted Array



Given an array of integers `A` sorted in non-decreasing order, return an array of the squares of each number, also in sorted non-decreasing order.

**Example 1:**

```text
Input: [-4,-1,0,3,10]Output: [0,1,9,16,100]
```

**Example 2:**

```text
Input: [-7,-3,2,3,11]Output: [4,9,9,49,121]
```

**Note:**

1. `1 <= A.length <= 10000`
2. `-10000 <= A[i] <= 10000`
3. `A` is sorted in non-decreasing order.

分析

排序平方值

可以直接sort，或者双指针，本题是sort数组，注意这里负数，两边都可能是最大的，所以要倒序塞入，appendleft

