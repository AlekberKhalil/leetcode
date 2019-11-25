# Find K Closest Elements

Given a sorted array, two integers `k` and `x`, find the `k` closest elements to `x` in the array. The result should also be sorted in ascending order. If there is a tie, the smaller elements are always preferred.

**Example 1:**  


```text
Input: [1,2,3,4,5], k=4, x=3
Output: [1,2,3,4]
```

**Example 2:**  


```text
Input: [1,2,3,4,5], k=4, x=-1
Output: [1,2,3,4]
```

**Note:**  


1. The value k is positive and will always be smaller than the length of the sorted array.
2. Length of the given array is positive and will not exceed 104
3. Absolute value of elements in the array and x will not exceed 104

**UPDATE \(2017/9/19\):**  
The arr parameter had been changed to an **array of integers** \(instead of a list of integers\). **Please reload the code definition to get the latest changes**.

分析

二分：找到start, 返回【start,start+k\]，花花模板

{% embed url="https://leetcode.com/problems/find-k-closest-elements/discuss/133604/Clean-O\(logN\)-solution-in-Python" %}

```text
class Solution:
    def findClosestElements(self, arr: List[int], k: int, x: int) -> List[int]:
        l,r = 0,len(arr)-k
        while l < r:
            m = (l+r)//2
            if x-arr[m] > arr[m+k]-x:
                l = m+1
            else:
                r = m
        return arr[l:l+k]
            
        
```



简单双指针易理解

注意边界 r+1

{% embed url="https://leetcode.com/problems/find-k-closest-elements/discuss/202785/Very-simple-Java-O\(n\)-solution-using-two-pointers" %}

```text
class Solution:
    def findClosestElements(self, arr: List[int], k: int, x: int) -> List[int]:
        l,r = 0,len(arr)-1
        while r - l >=k:
            
            if x-arr[l] > arr[r]-x:
                l += 1
            else:
                r -= 1
        return arr[l:r+1]
            
        
```



