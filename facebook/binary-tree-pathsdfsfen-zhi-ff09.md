# Binary Tree Paths\(dfs,分治）

Given a binary tree, return all root-to-leaf paths.

**Note:** A leaf is a node with no children.

**Example:**

```text
Input:   1 /   \2     3 \  5Output: ["1->2->5", "1->3"]Explanation: All root-to-leaf paths are: 1->2->5, 1->3
```

分析

注意此处返回有root == null和**root是叶节点2**个情况。

```text
if not root.left and not root.right 错的一塌糊涂！！！！！
```

dfs带path 和ret，返回void.

分治 return root.val+L+R

dfs：返回时候考虑当前node做头和做尾的情况，子调用时候不考虑自己。

```text
# Definition for a binary tree node.# class TreeNode:#     def __init__(self, x):#         self.val = x#         self.left = None#         self.right = Noneclass Solution:    def binaryTreePaths(self, root):        """        :type root: TreeNode        :rtype: List[str]        """        ret = []        if not root:            return ret        self.dfs(root,ret,"")        return list(ret)    def dfs(self,root,ret,path):        if not root.left and not root.right:            path+=str(root.val)            ret.append(path)            return        path+=str(root.val)+"->"        if root.left:            self.dfs(root.left,ret,path)        if root.right:            self.dfs(root.right,ret,path)        # path.pop()
```

分治：结束返回只考虑自己，往下走分支时候考虑把自己加入子调用。

```text
# Definition for a binary tree node.# class TreeNode:#     def __init__(self, x):#         self.val = x#         self.left = None#         self.right = Noneclass Solution:    def binaryTreePaths(self, root):        """        :type root: TreeNode        :rtype: List[str]        """        ret = []        if not root:            return []        if not root.left and not root.right:            return [str(root.val)]        ret+=[str(root.val)+"->"+i for i in self.binaryTreePaths(root.left)]        ret+=[str(root.val)+"->"+i for i in self.binaryTreePaths(root.right)]        return ret
```

