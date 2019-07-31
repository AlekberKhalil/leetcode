# Subsets II

Given a collection of integers that might contain duplicates,**nums**, return all possible subsets.

**Note:**The solution set must not contain duplicate subsets.

For example,  
If**nums**=`[1,2,2]`, a solution is:

```text
[
  [2],
  [1],
  [1,2,2],
  [2,2],
  [1,2],
  []
]
```

分析

Unique subset

遇到没有连续取同样数的时候要continue。（要取第三个2，必须取了前面的2，顺序不可乱）。所以添加了visited。

一定要排序！！！

可能visited也不用加，直接判断本层不能连续取同一个数字就好？

答案

```text
class Solution {
    public List<List<Integer>> subsetsWithDup(int[] nums) {
       List<List<Integer>> ret = new ArrayList<List<Integer>>();
        List<Integer> path = new ArrayList<Integer>();

        if(nums.length == 0)//下面dfs无论如何都会加一个空集，
            ret.add(path);
        boolean[] visited = new boolean[nums.length];
        Arrays.sort(nums);//一定要排序
        dfs(nums, ret, path, 0, visited);

        return ret;
        }

    private void dfs(int[] nums, List<List<Integer>> ret, List<Integer> path, int pos, boolean[] visited){

        ret.add(new ArrayList<Integer>(path));

        for(int i = pos; i < nums.length; i++){
            if(i != pos && nums[i] == nums[i - 1] && !visited[i - 1])
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

