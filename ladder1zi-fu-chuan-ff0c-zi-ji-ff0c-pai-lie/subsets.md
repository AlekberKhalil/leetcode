# subsets

Given a set of**distinct**integers,nums, return all possible subsets.

**Note:**The solution set must not contain duplicate subsets.

For example,  
If**nums**=`[1,2,3]`, a solution is:

```text
[  [3],  [1],  [2],  [1,2,3],  [1,3],  [2,3],  [1,2],  []]
```

分析

1.在dfs里Loop，不是在总函数里，记得加空集。等于是每层枚举可能性，一种是不取，另一种是取for loop里一个

2.不需要等Pos == nums.length再加入ret， 因为集合数目不定

```text
new 一个的原因在于 list 是可变对象，你加进去的时候只是指向对象的引用。ret.add(new ArrayList<Integer>(path));
```

```text
class Solution {    public List<List<Integer>> subsets(int[] nums) {     List<List<Integer>> ret = new ArrayList<List<Integer>>();        List<Integer> path = new ArrayList<Integer>();        if(nums.length == 0)//下面dfs无论如何都会加一个空集，            ret.add(path);        dfs(nums, ret, path, 0);        return ret;    }    private void dfs(int[] nums, List<List<Integer>> ret, List<Integer> path, int pos){        ret.add(new ArrayList<Integer>(path));        for(int i = pos; i < nums.length; i++){            path.add(nums[i]);            dfs(nums, ret, path, i+1);            path.remove(path.size()-1);        }    }}
```

