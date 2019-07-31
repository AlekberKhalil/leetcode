# Subsets II\(dfs\)

Given a collection of integers that might contain duplicates,_**nums**_, return all possible subsets \(the power set\).

**Note:**The solution set must not contain duplicate subsets.

**Example:**

```text
Input:
 [1,2,2]

Output:

[
  [2],
  [1],
  [1,2,2],
  [2,2],
  [1,2],
  []
]
```

这里subset带重复元素问题，一定记得排序。然后 i!=pos and nums\[i\]==nums\[i-1\]: continue

**python dfs:**

两种方法弹入弹出path

```text
path.append(nums[i])
self.dfs(nums,i+1,path,ret)
path.pop()

最后ret要copy path:     ret.append(list(path)) 或者 ret.append(path[:)
```

或者

```text
self.dfs(nums,i+1,path+[nums[i]],ret)

最后直接 ret.append(path)
```

方法1

```text
class Solution:
    def subsetsWithDup(self, nums):
        """
        :type nums: List[int]
        :rtype: List[List[int]]
        """
        ret = []
        nums.sort()
        self.dfs(nums,0,[],ret)

        return ret #list(set(ret))

    def dfs(self,nums, pos,path,ret):
        ret.append(list(path))

        for i in range(pos,len(nums)):
            if i!=pos and nums[i]==nums[i-1]:
                continue
            path.append(nums[i])
            self.dfs(nums,i+1,path,ret)
            path.pop()
```

方法2：

```text
class Solution:
    def subsetsWithDup(self, nums):
        """
        :type nums: List[int]
        :rtype: List[List[int]]
        """
        ret = []
        nums.sort()
        self.dfs(nums,0,[],ret)

        return ret #list(set(ret))

    def dfs(self,nums, pos,path,ret):
        ret.append(path)

        for i in range(pos,len(nums)):
            if i!=pos and nums[i]==nums[i-1]:
                continue            
            self.dfs(nums,i+1,path+[nums[i]],ret)
```

