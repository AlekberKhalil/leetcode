# Evaluate Division

Equations are given in the format `A / B = k`, where `A` and `B` are variables represented as strings, and `k` is a real number \(floating point number\). Given some queries, return the answers. If the answer does not exist, return `-1.0`.

**Example:**  
Given `a / b = 2.0, b / c = 3.0.`  
queries are: `a / c = ?, b / a = ?, a / e = ?, a / a = ?, x / x = ? .`  
return `[6.0, 0.5, -1.0, 1.0, -1.0 ].`

The input is: `vector<pair<string, string>> equations, vector<double>& values, vector<pair<string, string>> queries` , where `equations.size() == values.size()`, and the values are positive. This represents the equations. Return `vector<double>`.

According to the example above:

```text
equations = [ ["a", "b"], ["b", "c"] ],values = [2.0, 3.0],queries = [ ["a", "c"], ["b", "a"], ["a", "e"], ["a", "a"], ["x", "x"] ]. 
```

The input is always valid. You may assume that evaluating the queries will result in no division by zero and there is no contradiction.

分析

建图，分别{积：divisor1,devisor2} 2个都加入

dfs从起点起一步步拆分start，同时\*product.注意这里product起始是1.0不是1

```text
class Solution:    def calcEquation(self, equations: List[List[str]], values: List[float], queries: List[List[str]]) -> List[float]:        G = collections.defaultdict(list)        for e,v in zip(equations, values):            a,b = e            G[a].append((b,v))            G[b].append((a,1/v))                            def dfs(s,e,p,visited):            if s not in G or e not in G or s in visited:                return -1            if s == e:                return p            visited.add(s)            for n,v in G[s]:                temp = dfs(n,e,p*v,visited)                if temp!=-1:                    return temp            return -1         return[dfs(a,b,1.0,set()) for a,b in queries]              
```



