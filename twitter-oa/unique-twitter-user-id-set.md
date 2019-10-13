# Unique Twitter User Id Set



Twitter needs user ids to be unique and while assigning the user ids to its customers, Twitter wants to have the sum of the user ids to be minimum.  
Given an array of random user ids for n users, increment any duplicate elements untils all the user ids are unique and ensure that their sum is minimum.

#### Example

```text
Example:
Input:
arr = [3, 2, 1, 2, 7]
output: 17
Explanation：if arr = [3, 2, 1, 2, 7], then arr(unique) = [3, 2, 1, 4, 7] and its user ids sum to a minimal value of 3 + 2 + 1 + 4 + 7 = 17
```

分析

arr sort，每次记录当前可用最小的id-&gt;low, max\(low,cur\)。就是pre id ++

```text
class Solution:
    """
    @param arr: a integer array
    @return: return ids sum is minimum.
    """
    def UniqueIDSum(self, arr):
        # write your code here
        res = low = 0
        arr.sort()
        for i in arr:
            low = max(low,i)
            res+=low
            low+=1
        return res        
```

只能增加，while 内 ++,直到valid id 加入set

```text
class Solution:
    """
    @param arr: a integer array
    @return: return ids sum is minimum.
    """
    def UniqueIDSum(self, arr):
        # write your code here
        ids = set()
        res = 0
        for i in arr:
            while i in ids:
                i+=1
            ids.add(i)
            res +=i
        return res
        
```



