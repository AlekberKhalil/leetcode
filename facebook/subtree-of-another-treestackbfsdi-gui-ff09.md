# Subtree of Another Tree\(stack,bfs,递归）

```text
Given two non-empty binary trees s and t, check whether tree t has exactly the same structure and node values with a subtree of s. A subtree of s is a tree consists of a node in s and all of this node's descendants. The tree s could also be considered as a subtree of itself.

Example 1:
Given tree s:

     3
    / \
   4   5
  / \
 1   2
Given tree t:
   4 
  / \
 1   2
Return true, because t has the same structure and node values with a subtree of s.
Example 2:
Given tree s:

     3
    / \
   4   5
  / \
 1   2
    /
   0
Given tree t:
   4
  / \
 1   2
Return false.
```

分析

母树用stack或者bfs遍历，找到相等子树然后递归

stack

```text
class Solution:
    def isSubtree(self, s, t):
        """
        :type s: TreeNode
        :type t: TreeNode
        :rtype: bool
        """
        stack = [s]
        while stack:
            cur = stack.pop()
            if cur.val == t.val:
                if self.check(cur, t):
                    return True
            if cur.left:
                stack.append(cur.left)
            if cur.right:
                stack.append(cur.right)

        return False



    def check(self, s, t):
        if not s and not t:
            return True
        if s and t and s.val == t.val and self.check(s.left, t.left) and self.check(s.right, t.right):
            return True
        return False
```

bfs \(deque\)

```text
class Solution:
    def isSubtree(self, s, t):
        """
        :type s: TreeNode
        :type t: TreeNode
        :rtype: bool
        """
        q = collections.deque([s])
        while q:
            size = len(q)
            for i in range(size):
                cur = q.popleft()
                if cur.val == t.val and self.check(cur,t):
                    return True
                if cur.left:
                    q.append(cur.left)
                if cur.right:
                    q.append(cur.right)
        return False



    def check(self, s, t):
        if not s and not t:
            return True
        if s and t and s.val == t.val and self.check(s.left, t.left) and self.check(s.right, t.right):
            return True
        return False
```

