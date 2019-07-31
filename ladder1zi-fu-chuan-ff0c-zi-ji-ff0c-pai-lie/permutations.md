# Permutations

Given a collection of**distinct**numbers, return all possible permutations.

For example,  
`[1,2,3]`have the following permutations:

```text
[
  [1,2,3],
  [1,3,2],
  [2,1,3],
  [2,3,1],
  [3,1,2],
  [3,2,1]
]
```

分析

还是在dfs里for loop，从0-&gt;n不包括已经加入的数字。 Path.size\(\) == nums.length 就可以加入。不是pos == nums.length

答案

```text
class Solution {
    public List<List<Integer>> permute(int[] nums) {
    List<List<Integer>> ret = new ArrayList<List<Integer>>();
        List<Integer> path = new ArrayList<Integer>();

        dfs(nums, ret, path, 0);

        return ret;
    }

    private void dfs(int[] nums, List<List<Integer>> ret, List<Integer> path, int pos){
        if(path.size() == nums.length){
            ret.add(new ArrayList<Integer>(path));
        }       

        for(int i = 0; i < nums.length; i++){
            if(path.contains(nums[i]))
                continue;
            path.add(nums[i]);
            dfs(nums, ret, path, i+1);
            path.remove(path.size()-1);
        }
    }
}
```

