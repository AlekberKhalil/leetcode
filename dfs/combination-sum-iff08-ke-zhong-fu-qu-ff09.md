# Combination Sum I（可重复取）

Given a set of candidate numbers \(_**C**_\) and a target number \(_**T**_\), find all unique combinations in_**C**\_where the candidate numbers sums to_**T**\_.

The**same**repeated number may be chosen from\_**C**\_unlimited number of times.

## Example

Given candidate set`[2,3,6,7]`and target`7`, a solution set is:

```text
[7][2, 2, 3]
```

## Notice

```text
All numbers (including target) will be positive integers.Elements in a combination (a1, a2, … , ak) must be in non-descending order. (ie, a1 ≤ a2 ≤ … ≤ ak).The solution set must not contain duplicate combinations.
```

分析：

单数可重复取问题

* 要去重，用set。
* 要排序为了后面target&lt;num\[i\]可以直接返回，因为后面更大无需比了。

```text
class Solution:    """    @param candidates: A list of integers    @param target: An integer    @return: A list of lists of integers    """    def combinationSum(self, candidates, target):        # write your code here        candidates = sorted(list(set(candidates)))#排序和去重复，比如3个1只要一个        ret = []        self.dfs(candidates, target, ret, [], 0)        return ret    def dfs(self,candidates, target, ret, path, start):        if target == 0:            ret.append(list(path))        for i in range(start,len(candidates)):            if candidates[i] > target:#此处可以直接返回因为已排序，当前i不行的话后面更大                return            path.append(candidates[i])            self.dfs(candidates, target-candidates[i], ret, path, i)            path.pop()
```

