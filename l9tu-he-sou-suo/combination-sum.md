# Combination Sum

Given a**set**of candidate numbers \(**C**\)**\(without duplicates\)**and a target number \(**T**\), find all unique combinations in**C**where the candidate numbers sums to**T**.

The**same**repeated number may be chosen from**C**unlimited number of times.

**Note:**

* All numbers \(including target\) will be positive integers.
* The solution set must not contain duplicate combinations.

For example, given candidate set`[2, 3, 6, 7]`and target`7`,  
A solution set is:

```text
[
  [7],
  [2, 2, 3]
]
```

分析

带有pos的DFS，没pos的话会把233和332看成不同的path，导致最后结果有重复。

可能以后除了Permutation外，都要带pos来去重复。

DFS可以从当前i开始，因为允许当前元素重复。

```text
class Solution {
    public List<List<Integer>> combinationSum(int[] candidates, int target) {
        List<List<Integer>> ret = new ArrayList<>();
        if(candidates == null ||  candidates.length == 0)
            return ret;
        List<Integer> path = new ArrayList<Integer>();
        dfs(candidates, path, ret, target, 0 );
        return ret;
    }

    public void dfs(int[] candidates, List<Integer> path, List<List<Integer>> ret, int sum,  int pos){
        if(sum < 0) 
            return;
        if(sum == 0){
            if(!ret.contains(path))
            ret.add(new ArrayList<Integer>(path));
            return;
        }
        for(int i = pos; i < candidates.length; i ++){
            path.add(candidates[i]);
            dfs(candidates, path, ret, sum - candidates[i], i);//pos从i开始，因为可以重复。
            path.remove(path.size() - 1);
        }
    }
}
```

