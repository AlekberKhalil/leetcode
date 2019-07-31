# Permutations II

Given a collection of numbers that might contain duplicates, return all possible unique permutations.

For example,  
`[1,1,2]`have the following unique permutations:

```text
[
  [1,1,2],
  [1,2,1],
  [2,1,1]
]
```

分析

和前面一样，用visited数组判断重复数字是否连续。也排序。

```text
class Solution {
    public List<List<Integer>> permuteUnique(int[] nums) {
     List<List<Integer>> ret = new ArrayList<List<Integer>>();
        List<Integer> path = new ArrayList<Integer>();

        Arrays.sort(nums);
        boolean[] visited = new boolean[nums.length];
        dfs(nums, ret, path, 0, visited);

        return ret;
    }

    private void dfs(int[] nums, List<List<Integer>> ret, List<Integer> path, int pos, boolean[] visited){
        if(path.size() == nums.length){
            ret.add(new ArrayList<Integer>(path));
        }       

        for(int i = 0; i < nums.length; i++){
            if(visited[i] || i != 0 && nums[i] == nums[i - 1] && !visited[i - 1])
                continue;
            path.add(nums[i]);
            visited[i] = true;
            dfs(nums, ret, path, i+1, visited);
            visited[i] = false;
            path.remove(path.size()-1);
        }
    }
}
```

