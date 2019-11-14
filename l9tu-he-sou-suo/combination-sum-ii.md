# Combination Sum II

Given a collection of candidate numbers \(**C**\) and a target number \(**T**\), find all unique combinations in**C**where the candidate numbers sums to**T**.

Each number in**C**may only be used**once**in the combination.

**Note:**

* All numbers \(including target\) will be positive integers.
* The solution set must not contain duplicate combinations.

For example, given candidate set`[10, 1, 2, 7, 6, 1, 5]`and target`8`,  
A solution set is:

```text
[
  [1, 7],
  [1, 2, 5],
  [2, 6],
  [1, 1, 6]
]
```

分析

注意这里 target == 0 加入res . 《0或者重复时候，不一样处理

```text
class Solution:
    def combinationSum2(self, c: List[int], target: int) -> List[List[int]]:
        c.sort()
        res = []
        n=len(c)
        def dfs(pos,path,target):
            if target == 0:
                res.append(path)
            
            for i in range(pos,n ):
                if c[i] > target:
                    return
                
                if i!=pos and c[i]==c[i-1]:
                    continue #！！！！！！
                    
                dfs(i+1,path+[c[i]],target - c[i])
        dfs(0,[],target)             
        return res
                    
                
        
```

DSF带去重和带Pos：candidates\[i - 1\] == candidates\[i\] && !visited\[i-1\]

```text
class Solution {
    public List<List<Integer>> combinationSum2(int[] candidates, int target) {
       List<List<Integer>> ret = new ArrayList<>();
        if(candidates == null ||  candidates.length == 0)
            return ret;
        List<Integer> path = new ArrayList<Integer>();
        boolean[] visited = new boolean[candidates.length];
        Arrays.sort(candidates);
        dfs(candidates, path, ret, target, 0 , visited);
        return ret;
    }

    public void dfs(int[] candidates, List<Integer> path, List<List<Integer>> ret, int sum,  int pos, boolean[] visited){
        if(sum < 0) 
            return;
        if(sum == 0){
            if(!ret.contains(path))
            ret.add(new ArrayList<Integer>(path));
            return;
        }
        for(int i = pos; i < candidates.length; i ++){
            if(visited[i] || (i != 0 && candidates[i - 1] == candidates[i] && !visited[i-1])){
                continue;
            }else{
                path.add(candidates[i]);
                visited[i] = true;
                dfs(candidates, path, ret, sum - candidates[i], i + 1,visited);
                path.remove(path.size() - 1);
                visited[i] = false;
            }           
        }
    }
}
```

