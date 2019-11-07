# Count of Range Sum

Given an integer array`nums`, return the number of range sums that lie in`[lower, upper]`inclusive.  
Range sum`S(i, j)`is defined as the sum of the elements in`nums`between indices`i`and`j`\(`i`≤`j`\), inclusive.

**Note:**  
A naive algorithm ofO\(n2\) is trivial. You MUST do better than that.

**Example:**

```text
Input: nums = [-2,5,-1], lower = -2, upper = 2,Output: 3 Explanation: The three ranges are : [0,0], [2,2], [0,2] and their respective sums are: -2, -1, 2.
```

分析

```text
Sum[k] is the sum of first k numbers. O(N^2) solution isfor j in range(n + 1):    for i in range(j):        if lower <= Sum[j] - Sum[i] <= upper: res += 1This is equal to:collection = emptyfor sum_j in Sum:    sum_i_count = how many sum_i in this collection that sum_j - upper <= sum_i <= sum_j - lower    res += sum_i_count    put sum_j into this collection
```

算presum，然后遍历sum来Update bitTree，这里用的Index是该sum在sorted后sum arr的index。每加入一个sum，就提高该sum和parent sum的权重。最后get就是权重相减。

```text
class Solution:    def countRangeSum(self, nums: List[int], lower: int, upper: int) -> int:        n = len(nums)        sums = [0] * (n+1)        bitTree = [0]*(n+2)        for i,v in enumerate(nums):            sums[i+1] = sums[i]+v         sortSums = sorted(sums)        res = 0        def update(i):            while i <= n+1:                bitTree[i] += 1                i += i&-i        def query(i):            sm = 0            while i > 0:                sm += bitTree[i]                i-=i&-i            return sm        for s in sums:            res += query(bisect.bisect_right(sortSums,s-lower)) - query(bisect.bisect_left(sortSums,s-upper))            update(bisect.bisect_left(sortSums,s)+1)        return res
```

分治法

presum数组分半，左右分治相加之后，计算跨越左右的部分。

固定左边在Mid前，右边i,j分别算max和min可达范围。左边固定点在\[lo,mid\]之间loop

```text
class Solution:    def countRangeSum(self, nums: List[int], lower: int, upper: int) -> int:        sums = [0]        for i in nums:            sums.append(sums[-1]+i)        def helper(l,r): #前闭后开区间            cnt = 0            mid = (l+r)//2            if l == mid:                return 0            cnt = helper(l,mid) + helper(mid,r)            i = j = mid            for left in sums[l:mid]:                while i < r and sums[i] -left < lower:                    i += 1                while j < r and sums[j] -left <=upper:                    j += 1                cnt += j-i            sums[l:r] = sorted(sums[l:r]) #因为有序，所以上面才能顺序后移。            return cnt        return helper(0,len(sums))
```

segment tree 用sum 值范围， 不是Index做范围，count做val返回。对比前面直接Index建树，不是值范围。

query root在范围内直接返回root

记得update里要返回 min = max = val

```text
class Node:    def __init__(self,mn,mx):        self.mn = mn        self.mx = mx        self.cnt = 0        self.left = None        self.right = Noneclass Solution:    # def __init__(self,nums):    root = None    def buildTree(self,nums,s,e):        if s>e:            return None        node = Node(nums[s],nums[e])        if s == e:            return node        mid = (s+e)//2        l = self.buildTree(nums,s,mid)        r = self.buildTree(nums,mid+1,e)        node.left,node.right = l,r        return node    def update(self,val,root=None):        root = root or self.root        # if not root:        #     return                if root.mn<=val<=root.mx:#不像前面左右加更新root值，因为找范围没有特定数，而且这里范围内就加了            root.cnt += 1               if val == root.mn == root.mx:                return root.cnt            self.update(val,root.left)            self.update(val,root.right)    def query(self,mn,mx,root=None):        root = root or self.root        # if not root:        #     return 0        if mn > root.mx or mx<root.mn:            return 0        if mn <= root.mn and mx>=root.mx:            return root.cnt        return self.query(mn, mx, root.left) + self.query(mn,mx,root.right)    def countRangeSum(self, nums: List[int], lower: int, upper: int) -> int:        sums = [0] * (len(nums)+1)        for i,v in enumerate(nums):            # sums[i] = sums[i-1]+v if i > 0 else v            sums[i+1] = sums[i]+v        sortSums = sorted(set(sums))        self.root = self.buildTree(sortSums,0,len(sortSums)-1)        res = 0        # sums = [0]+sums[:]        sm = sums[-1]        for i in nums[::-1]:            self.update(sm)            sm -= i            res += self.query(sm+lower,sm+upper)        return res
```

