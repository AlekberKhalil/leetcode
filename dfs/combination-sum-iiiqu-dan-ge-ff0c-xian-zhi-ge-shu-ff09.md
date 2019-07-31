# Combination Sum III\(取单个，限制个数）

Find all possible combinations of k numbers that add up to a number n, given that only numbers from 1 to 9 can be used and each combination should be a unique set of numbers.

Note:

All numbers will be positive integers.  
The solution set must not contain duplicate combinations.  
Example 1:

Input: k = 3, n = 7  
Output: \[\[1,2,4\]\]  
Example 2:

Input: k = 3, n = 9  
Output: \[\[1,2,6\], \[1,3,5\], \[2,3,4\]\]

分析

不可重复取，加上条件

```text
class Solution:
    """
    @param num: Given the candidate numbers
    @param target: Given the target number
    @return: All the combinations that sum to target
    """
    def combinationSum3(self, k,n):
        # write your code here

        ret = []
        self.dfs(k,n, ret, [], 1)
        return ret

    def dfs(self, k,n, ret, path, start):
        if n == 0 and k == 0:
            ret.append(list(path))
            return

        for i in range(start,10):
            if i > n:
                return

            path.append(i)
            self.dfs(k-1, n-i, ret, path, i+1)
            path.pop()
```

