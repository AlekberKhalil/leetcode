# Populating Next Right Pointers in Each Node II\(BFS\)

Given a binary tree

```text
struct TreeLinkNode {  TreeLinkNode *left;  TreeLinkNode *right;  TreeLinkNode *next;}
```

Populate each next pointer to point to its next right node. If there is no next right node, the next pointer should be set to`NULL`.

Initially, all next pointers are set to`NULL`.

**Note:**

* You may only use constant extra space.
* Recursive approach is fine, implicit stack space does not count as extra space for this problem.

**Example:**

Given the following binary tree,

```text
     1   /  \  2    3 / \    \4   5    7
```

After calling your function, the tree should look like:

```text
  1 -> NULL   /  \  2 -> 3 -> NULL / \    \4-> 5 -> 7 -> NULL
```

分析

BFS，最后一个node记得用i== n-1判断

```text
# Definition for binary tree with next pointer.# class TreeLinkNode:#     def __init__(self, x):#         self.val = x#         self.left = None#         self.right = None#         self.next = Noneclass Solution:    # @param root, a tree link node    # @return nothing    def connect(self, root):        if not root:            return root        q=[root]        while q:            n = len(q)            for i in range(n):                cur = q.pop(0)                if i == n-1:                    cur.next =None                else:                    cur.next = q[0]                if cur.left:                    q.append(cur.left)                if cur.right:                    q.append(cur.right)
```

利用链表特性。每层都建个dummy。然后dummy指向前一层root。左右依次加入链表

```text
class Solution:   
	def connect(self, root):        
		while root:
			dummy = TreeLinkNode(0)
			curc = dummy
			while root:根据本层的遍历连接孩子层
					if root.left:
			        curc.next = root.left
			        curc = curc.next
			    if root.right:
			        curc.next = root.right
			        curc = curc.next
			    root = root.next
			root = dummy.next	#root设置为孩子层	
```

DFS Recursive

```text
"""
# Definition for a Node.
class Node:
    def __init__(self, val, left, right, next):
        self.val = val
        self.left = left
        self.right = right
        self.next = next
"""
class Solution:
    def connect(self, root: 'Node') -> 'Node':
        
        if not root:
            return None
        p = pre = Node(-1,None,None,None)
        res = root
        while root:
            if root.left:
                pre.next = root.left
                pre = pre.next
            if root.right:
                pre.next = root.right
                pre = pre.next
            root = root.next
        self.connect(p.next)
        return res
                    
```

