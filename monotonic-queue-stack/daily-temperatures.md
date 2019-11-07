# Daily Temperatures

Given a list of daily temperatures `T`, return a list such that, for each day in the input, tells you how many days you would have to wait until a warmer temperature. If there is no future day for which this is possible, put `0` instead.

For example, given the list of temperatures `T = [73, 74, 75, 71, 69, 72, 76, 73]`, your output should be `[1, 1, 4, 2, 1, 1, 0, 0]`.

**Note:** The length of `temperatures` will be in the range `[1, 30000]`. Each temperature will be an integer in the range `[30, 100]`.

分析

单调递增，遇到大的，弹出前面小的，并且存储小的结果

stack里存的是Index

```text
class Solution:
    def dailyTemperatures(self, T: List[int]) -> List[int]:
        s = []
        res = [0]*len(T)
        for i,x in enumerate(T):           
            while s and T[s[-1]] < x:
                lastIndex = s.pop()
                res[lastIndex] = i-lastIndex
            s.append(i)
        return res
                
                
                
        
```

