# Number of restaurants双指针

## Description

Give a`List`of data representing the coordinates`[x,y]`of each restaurant and the customer is at the origin`[0,0]`. Find the`n`restaurants closest to the customer firstly. Then you need to pick n restaurants which appeare firstly in the`List`and the distance between the restaurant and the customer can't more than the longest distance in the`n`closest restaurants. Return their coordinates in the original order.

1.Coordinates in range \[-1000,1000\]  
2.n&gt;0  
3.No same coordinates

Have you met this question in a real interview?

Yes

Problem Correction

## Example

```text
Given : n = 2 , List = [[0,0],[1,1],[2,2]]Return : [[0,0],[1,1]]
```

```text
Given : n = 3,List = [[0,1],[1,2],[2,1],[1,0]]Return :[[0,1],[1,2],[2,1]]
```

分析

其实就是找第k大，然后loop原数组顺序找出来k个比这个数小的

错了很久的是 q传入 时候被改变。顺序变了不能用q找出该有的顺序了。

```text
class Solution:    """    @param restaurant:    @param n:    @return: nothing    """    def nearestRestaurant(self, restaurant, n):        # Write your code here        q = []        res = []        if not restaurant or not n or n > len(restaurant):            return res         for ii,i in enumerate(restaurant):            q.append((ii,i[0]**2 + i[1]**2))        qq = q[:]        p = self.findNth(qq,0,len(q)-1,n)        cnt = 0        for v in q:            if v[1] <= p[1] and cnt < n:                res.append(restaurant[v[0]])                cnt +=1        return res    def findNth(self,q,s,e,n):        # if s==e:        #     return q[s]        l ,r = s,e        p = q[l]        while l < r:            while l < r and q[r][1] >= p[1]:                r -= 1            q[l] = q[r]            while l < r and q[l][1] <= p[1]:                l += 1            q[r] = q[l]        q[l] = p        if l == n-1:            return q[l]        elif l < n-1:            return self.findNth(q,l+1,e,n)        else:            return self.findNth(q,s,l-1,n)
```

