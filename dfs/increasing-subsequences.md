# Increasing Subsequences

Given an integer array, your task is to find all the different possible increasing subsequences of the given array, and the length of an increasing subsequence should be at least 2 .

**Example:**

```text
Input:
 [4, 6, 7, 7]

Output:
 [[4, 6], [4, 7], [4, 6, 7], [4, 6, 7, 7], [6, 7], [6, 7, 7], [7,7], [4,7,7]]
```

**Note:**

1. The length of the given array will not exceed 15.
2. The range of integer in the given array is \[-100,100\].
3. The given array may contain duplicates, and two equal integers should also be considered as a special case of increasing sequence.

分析

这里好像可以用subset方法？

dfs带start参数

去重在本层for 保持一个set，使用过的数字不再用。比较combination sum去重，直接sort，和前面比较相等就跳过，

这里不能sort，因为要顺序比较大小。只能用set来去重。

```text
class Solution:
    def findSubsequences(self, nums: List[int]) -> List[List[int]]:
        res = []
        ll = len(nums)
        def dfs(path,idx):
            if len(path) >=2 :
                res.append(path)
            ss = set()#在本层一样的数字不能再选 
            for i in range(idx,ll):        
                if (not path or nums[i] >= path[-1]) and nums[i] not in ss:
                    ss.add(nums[i])
                    dfs(path + [nums[i]],i + 1)

        dfs([],0)
        return res
```

