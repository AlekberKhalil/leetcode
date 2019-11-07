# Range Sum Query - Mutable

Given an integer arraynums, find the sum of the elements between indices i and j\(i≤j\), inclusive.

Theupdate\(i, val\)function modifiesnumsby updating the element at indexitoval.

**Example:**

```text
Given nums = [1, 3, 5]

sumRange(0, 2) ->9
update(1, 2)
sumRange(0, 2) ->8
```

**Note:**

1. The array is only modifiable by the

   update

   function.

2. You may assume the number of calls to

   update

   and

   sumRange

   function is distributed evenly.

分析

线段树sum

如果是matrix的话，就是左上右下定位。然后每次分成4段算，4个孩子。

```text
class SegmentNode:
    def __init__(self, s,e,val):
        self.s = s
        self.e = e
        self.val = val
        self.left = None
        self.right = None

class NumArray:

    def buildTree(self,s,e,nums):        
        if s == e:
            return SegmentNode(s,e,nums[s])
        mid =  s+ (e-s) // 2

        l = self.buildTree(s, mid, nums)
        r = self.buildTree(mid+1,e,nums)

        root =  SegmentNode(s,e,l.val + r.val)
        root.left = l
        root.right = r
        return root    


    def __init__(self, nums: List[int]):
        self.nums = nums
        n = len(nums)
        if n > 0:
            self.root = self.buildTree(0,n-1,nums)


    def update(self,  i: int, val: int,  root = None) -> None:
        if not root:
            root = self.root
        if root.s == root.e == i:
            root.val = val #错很久
            return 
        mid = root.s + (root.e-root.s) // 2
        if i <= mid:
            self.update(i,val, root.left)
        else :
            self.update(i,val, root.right)
        root.val = root.left.val + root.right.val        

    def sumRange(self, i: int, j: int, root = None) -> int:
        if not root:
            root = self.root
        if i == root.s and j == root.e:
            return root.val
        mid = root.s + (root.e-root.s)//2
        if j <= mid:
            return self.sumRange(i,j,root.left)
        elif i > mid:
            return self.sumRange(i,j,root.right)
        else:
            return self.sumRange(i,mid, root.left)+self.sumRange(mid+1,j, root.right)






# Your NumArray object will be instantiated and called as such:
# obj = NumArray(nums)
# obj.update(i,val)
# param_2 = obj.sumRange(i,j)
```

binary index tree

初始化时候，或者duplicate 一部分update的code, 建树，但是不改变Nums

或者直接call update，但是更改新的arr\[0\]，不能改原nums

```text
class NumArray:

    def __init__(self, nums: List[int]):
        self.n = len(nums)
        self.bts = [0]*(self.n+1)
        self.arr = [0]*(self.n)
        for i, v in enumerate(nums):
            # k = i+1
            # while k < self.n+1:
            #     self.bts[k] += v
            #     k += (k&(-k))
            self.update(i,v) 



    def update(self, i: int, val: int) -> None:
        diff = val - self.arr[i]
        self.arr[i] = val
        i = i+1
        while i < self.n+1:
            self.bts[i] +=diff
            i+= i &(-i)


    def sumRange(self, i: int, j: int) -> int:
        def query(i):
            sm = 0
            i=i+1
            while i > 0:
                sm += self.bts[i]
                i -= i&(-i)
            return sm
        return query(j)-query(i-1)



# Your NumArray object will be instantiated and called as such:
# obj = NumArray(nums)
# obj.update(i,val)
# param_2 = obj.sumRange(i,j)
```

