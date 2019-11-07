# Two Sum IV - Input is a BST\(bfs+set\)

Given a Binary Search Tree and a target number, return true if there exist two elements in the BST such that their sum is equal to the given target.

**Example 1:**

```text
Input:

    5
   / \
  3   6
 / \   \
2   4   7

Target = 9


Output:
 True
```

**Example 2:**

```text
Input:

    5
   / \
  3   6
 / \   \
2   4   7

Target = 28
```

分析

two sum。一个queue存元素，一个set存值。bfs 每次检查k-root.val是否在set里

```text
class Solution:
       def findTarget(self, root, k):
        """
        :type root: TreeNode
        :type k: int
        :rtype: bool
        """
        if not root:
            return False
        s = set()
        q = collections.deque([root])
        while q:
            n = q.popleft()
            if n:
                if k - n.val in s:
                    return True
                s.add(n.val)
                q.append(n.left)
                q.append(n.right)

        return False
```

