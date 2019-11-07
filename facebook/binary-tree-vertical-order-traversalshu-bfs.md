# Binary Tree Vertical Order Traversal\(树bfs）

Given a binary tree, return the vertical order traversal of its nodes' values. \(ie, from top to bottom, column by column\).

If two nodes are in the same row and column, the order should be from**left to right**.

## Example

Given binary tree`{3,9,20,#,#,15,7}`

```text
   3  /\ /  \ 9  20    /\   /  \  15   7
```

Return its vertical order traversal as:  
`[[9],[3,15],[20],[7]]`

Given binary tree`{3,9,8,4,0,1,7}`

```text
     3    /\   /  \   9   8  /\  /\ /  \/  \ 4  01   7
```

Return its vertical order traversal as:  
`[[4],[9],[3,0,1],[8],[7]]`

分析

如果是要求层顺序，使用bfs，如果要求root和l,r顺序，考虑pre in post

这题不知道为什么dfs不行，可能因为顺序？

**dict可以用负数做Key和排序**

```text
"""Definition of TreeNode:class TreeNode:    def __init__(self, val):        self.val = val        self.left, self.right = None, None"""class Solution:    """    @param root: the root of tree    @return: the vertical order traversal    """    def verticalOrder(self, root):        # write your code here        if not root:            return []        dict = collections.defaultdict(list)        q = collections.deque()        q.append((root,0))        while q:            size = len(q)            for i in range(size):                cur = q.popleft()                dict[cur[1]].append(cur[0].val)                if cur[0].left:                    q.append((cur[0].left,cur[1]-1))                if cur[0].right:                    q.append((cur[0].right,cur[1]+1))        ret = []        for key in sorted(dict.keys()):            ret.append(dict[key])        return ret
```

