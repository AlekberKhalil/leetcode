# Construct Binary Search Tree from Preorder Traversal



Return the root node of a binary **search** tree that matches the given `preorder` traversal.

_\(Recall that a binary search tree is a binary tree where for every node, any descendant of `node.left` has a value `<` `node.val`, and any descendant of `node.right` has a value `>` `node.val`.  Also recall that a preorder traversal displays the value of the `node` first, then traverses `node.left`, then traverses `node.right`.\)_

**Example 1:**

```text
Input: [8,5,1,7,10,12]
Output: [8,5,10,1,7,null,12]
```



分析

因为bst 所以左树《root.val&lt;右树

按照范围，左边第一个比max小的数字就是root，所以设置max，顺序找第一个数字 《=max，然后递归

```text
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def bstFromPreorder(self, p: List[int]) -> TreeNode:
        
        def helper(stop):
            if p and p[0] <= stop:
                root = TreeNode(p.pop(0))
                root.left = helper(root.val)
                root.right = helper(stop)
                return root
            
        #p.reverse()   
        return helper(max(p))
            
            
        
```

recursive

```text
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def bstFromPreorder(self, p: List[int]) -> TreeNode:
        if not p:
            return None
        if len(p) == 1:
            return TreeNode(p[0])
        root = TreeNode(p[0])
        i=1
        while i<len(p) and p[i]<root.val:
            i+=1
        root.left = self.bstFromPreorder(p[1:i])
        root.right = self.bstFromPreorder(p[i:])
        return root
        
            
            
        
```

