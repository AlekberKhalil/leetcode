# Count of Smaller Numbers After Self

You are given an integer arraynumsand you have to return a newcountsarray. Thecountsarray has the property where`counts[i]`is the number of smaller elements to the right of`nums[i]`.

**Example:**

```text
Input:
 [5,2,6,1]

Output:
[2,1,1,0] 

Explanation:

To the right of 5 there are 
2
 smaller elements (2 and 1).
To the right of 2 there is only 
1
 smaller element (1).
To the right of 6 there is 
1
 smaller element (1).
To the right of 1 there is 
0
 smaller element.
```

binary index tree

和后面reverse pair比较，正序update是因为提高的权重应该是比它大的数字（index比它高）。因为右边起，所以只有右边的数能让左边数权重变大

Nummap里存排序好的数，ordered num-&gt;ordered index

右边起，遇到数就更新树，让大于它的Parent的权重都+1.（index &gt; currrent i\)

```text
class BinaryIndexTree:
    def __init__(self,n):
        self.sums = [0]*(n+1)
    def update(self,i,v):        
        while i < len(self.sums):
            self.sums[i]+=v
            i += i&-i
    def query(self,i):
        sm = 0
        while i > 0 :
            sm += self.sums[i]
            i -= i&-i
        return sm

class Solution:        
    def countSmaller(self, nums: List[int]) -> List[int]:
        numMap = {v:i for i,v in enumerate(sorted(set(nums)))}

        tree,res = BinaryIndexTree(len(numMap)), []
        for i in reversed(nums):
            res.append(tree.query(numMap[i]))#当前数，范围不含本数。
            tree.update(numMap[i] + 1, 1) #当前数的parents都更新
        return res[::-1]
```

segment tree

也是排序建立map：ordered num-&gt;ordered index

倒序遍历，先得到范围前的sum,然后然后该数范围权重+=1

```text
class Node:
    def __init__(self,s,e):
        self.s = s
        self.e = e
        self.val = 0
        self.left = None
        self.right = None

class SegmentTree:
    def __init__(self,n):
        self.root = self.build(0,n-1)

    def build(self,s,e):
        if s > e:
            return
        node = Node(s,e)
        if s == e:
            return node
        m = (s+e)//2
        l = self.build(s,m)
        r = self.build(m+1,e)
        node.left,node.right,node.val = l,r,l.val+r.val
        return node


    def update(self,i,v,root=None):
        root = root or self.root
        if root.s==root.e==i:
            root.val += v #+= 提高权重而不是赋值
            return
        m = (root.s+root.e)//2
        if i <= m:
            self.update(i,v,root.left)
        else:
            self.update(i,v,root.right)
        root.val = root.left.val + root.right.val


    def query(self,l,r,root=None):
        root = root or self.root
        if l >root.e or r <root.s:
            return 0
        if root.s == l and root.e == r:
            return root.val
        m = (root.s+root.e)//2
        if r <= m:
            return self.query(l,r,root.left)
        elif l > m:
            return self.query(l,r,root.right)
        else:
            return self.query(l,m,root.left)+self.query(m+1,r,root.right)


class Solution:        
    def countSmaller(self, nums: List[int]) -> List[int]:
        numMap = {v:i for i,v in enumerate(sorted(set(nums)))}

        tree,res = SegmentTree(len(numMap)), []
        for i in reversed(nums):
            res.append(tree.query(0,numMap[i]-1))#该数前面的
            tree.update(numMap[i], 1) #该数提高本范围内权重
        return res[::-1]
```

