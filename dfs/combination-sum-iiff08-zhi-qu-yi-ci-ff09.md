# Combination Sum II（只取一次）

Given a collection of candidate numbers \(_C_\) and a target number \(_T_\), find all unique combinations in_C\_where the candidate numbers sums to\_T_.

Each number in\_C\_may only be used once in the combination.

## Example

Given candidate set`[10,1,6,7,2,1,5]`and target`8`,

A solution set is:

```text
[  [1,7],  [1,2,5],  [2,6],  [1,1,6]]
```

## Notice

```text
All numbers (including target) will be positive integers.Elements in a combination (a1, a2, … , ak) must be in non-descending order. (ie, a1 ≤ a2 ≤ … ≤ ak).The solution set must not contain duplicate combinations.
```

分析

单个元素只能取一次

不要set去重，但是还是要sort，为了后面剪枝，直接return

遇到n\[i-1\]==n\[i\]，只是当前数不行，continue就好，不要return

```text
class Solution:    """    @param num: Given the candidate numbers    @param target: Given the target number    @return: All the combinations that sum to target    """    def combinationSum2(self, num, target):        # write your code here        num = sorted(num)        ret = []        self.dfs(num, target, ret, [], 0)        return ret    def dfs(self, num, target, ret, path, start):        if target == 0:            return ret.append(list(path))        for i in range(start,len(num)):            if num[i] > target:                return            if i != start and num[i]==num[i-1]:                continue #只是当前数不行，剩下的还可以试， 不能return            path.append(num[i])            self.dfs(num, target-num[i], ret, path, i+1)            path.pop()
```

