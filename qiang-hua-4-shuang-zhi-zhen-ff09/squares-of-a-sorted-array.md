# Squares of a Sorted Array

Given an array of integers`A` sorted in non-decreasing order, return an array of the squares of each number, also in sorted non-decreasing order.

**Example 1:**

```text
Input: 
[-4,-1,0,3,10]
Output: 
[0,1,9,16,100]
```

**Example 2:**

```text
Input: 
[-7,-3,2,3,11]
Output: 
[4,9,9,49,121]
```

分析

可以从最大开始加入res，指针从左右2边开始

自己做法是找到第一个负数，然后左右展开

```text
class Solution:
    def sortedSquares(self, A: List[int]) -> List[int]:
        ll = len(A)
        res = [0]*ll
        left,right, p =0,ll-1, ll -1
        while p >=0:
            if A[left]**2 > A[right]**2:
                res[p] = A[left]**2
                left +=1
            else:
                res[p] = A[right]**2
                right -= 1
            p -= 1
        return res




#         idx = 0
#         ll = len(A)
#         res = []
#         for i in range(ll):
#             if A[i]>=0 and i>0:
#                 idx = i-1
#                 break

#         left,right = idx,idx+1
#         while left < right and left >=0 and right<ll:
#             if A[left]**2 == A[right]**2:
#                 res.append(A[left]**2)
#                 res.append(A[right]**2)
#                 left -=1
#                 right+=1
#             elif A[left]**2 > A[right]**2:
#                 res.append(A[right]**2)
#                 right += 1
#             else:
#                 res.append(A[left]**2)
#                 left -=1

#         while left >=0:
#             res.append(A[left]**2)
#             left -=1

#         while right<ll:
#             res.append(A[right]**2)
#             right += 1 
#         return res
```

