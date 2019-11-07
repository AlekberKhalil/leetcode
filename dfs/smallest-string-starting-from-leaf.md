# Smallest String Starting From Leaf

Given the`root`of a binary tree, each node has a value from`0`to`25`representing the letters`'a'`to`'z'`: a value of`0`represents`'a'`, a value of`1`represents`'b'`, and so on.

Find the lexicographically smallest string that starts at a leaf of this tree and ends at the root.

_\(As a reminder, any shorter prefix of a string is lexicographically smaller: for example,_`"ab"`_is lexicographically smaller than_`"aba"`_. A leaf of a node is a node that has no children.\)_

1. **Example 1:**

![](https://assets.leetcode.com/uploads/2019/01/30/tree1.png)

```text
Input: [0,1,2,3,4,3,4]Output: "dba"
```

**Example 2:**

![](https://assets.leetcode.com/uploads/2019/01/30/tree2.png)

```text
Input: [25,1,3,1,3,0,2]Output: "adz"
```

**Example 3:**

![](https://assets.leetcode.com/uploads/2019/02/01/tree3.png)

```text
Input: [2,2,1,null,1,0,null,0]Output: "abc"
```

**Note:**

```text
The number of nodes in the given tree will be between 1 and 8500.Each node in the tree will have a value between 0 and 25.
```

分析

不能分治，因为要比较后缀而不是前缀，前缀大小不能决定结果：\[\[[https://leetcode.com/problems/smallest-string-starting-from-leaf/discuss/244205/Divide-and-conquer-technique-doesn't-work-for-this-problem\]\(https://leetcode.com/problems/smallest-string-starting-from-leaf/discuss/244205/Divide-and-conquer-technique-doesn't-work-for-this-problem\]\(https://leetcode.com/problems/smallest-string-starting-from-leaf/discuss/244205/Divide-and-conquer-technique-doesn't-work-for-this-problem\]%28https://leetcode.com/problems/smallest-string-starting-from-leaf/discuss/244205/Divide-and-conquer-technique-doesn't-work-for-this-problem\)\](https://leetcode.com/problems/smallest-string-starting-from-leaf/discuss/244205/Divide-and-conquer-technique-doesn't-work-for-this-problem]%28https://leetcode.com/problems/smallest-string-starting-from-leaf/discuss/244205/Divide-and-conquer-technique-doesn't-work-for-this-problem]%28https://leetcode.com/problems/smallest-string-starting-from-leaf/discuss/244205/Divide-and-conquer-technique-doesn't-work-for-this-problem]%28https://leetcode.com/problems/smallest-string-starting-from-leaf/discuss/244205/Divide-and-conquer-technique-doesn't-work-for-this-problem%29\)\)

```text
The expected answer is "ababz", while by divide-and-conqure we would get "abz".The problem here isstring X < string Ydoesn't guaranteeX + a < Y + awhere a is a character. e.g.:"ab" < "abab", but "abz" > "ababz"
```

这里path就是后缀，没有左右子树了就可以更新res

```text
# Definition for a binary tree node.# class TreeNode:#     def __init__(self, x):#         self.val = x#         self.left = None#         self.right = Noneclass Solution:    def smallestFromLeaf(self, root: TreeNode) -> str:                if not root:            return ""        res = "~"        def dfs(root,surfix):            nonlocal res            if not root:                return             c = chr(root.val+97)+surfix            if not root.left and not root.right and c < res:                                res = c            dfs(root.left, c)            dfs(root.right,c)        dfs(root,"")        return res
```

