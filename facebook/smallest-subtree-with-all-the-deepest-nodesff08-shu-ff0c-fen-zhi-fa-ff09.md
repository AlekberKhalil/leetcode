# Smallest Subtree with all the Deepest Nodes（树，分治法）

Given a binary tree rooted at`root`, the\_depth\_of each node is the shortest distance to the root.

A node is\_deepest\_if it has the largest depth possible among any node in theentire tree.

The subtree of a node is that node, plus the set of all descendants of that node.

Return the node with the largest depth such that it contains all the deepest nodes in its subtree.

**Example 1:**

```text
Input: [3,5,1,6,2,0,8,null,null,7,4]Output: [2,7,4]Explanation:We return the node with value 2, colored in yellow in the diagram.The nodes colored in blue are the deepest nodes of the tree.The input "[3, 5, 1, 6, 2, 0, 8, null, null, 7, 4]" is a serialization of the given tree.The output "[2, 7, 4]" is a serialization of the subtree rooted at the node with value 2.Both the input and output have TreeNode type.
```

分析：

根据题目返回，哪个子树大返哪个，一样大返自己。用分治得到左右子树，左右子树的结果来创造new result。这里结果用了一个result类。

```text
/** * Definition for a binary tree node. * public class TreeNode { *     int val; *     TreeNode left; *     TreeNode right; *     TreeNode(int x) { val = x; } * } */class Solution {    public TreeNode subtreeWithAllDeepest(TreeNode root) {        return dfs(root).node;    }    // Return the result of the subtree at this node.    public Result dfs(TreeNode node) {        if(node == null){            return new Result(0, node);        }        Result l = dfs(node.left);        Result r = dfs(node.right);        return l.dist > r.dist? new Result(l.dist + 1, l.node) :         l.dist == r.dist ?new Result(r.dist + 1, node) :            new Result(r.dist + 1, r.node) ;    }}/** * The result of a subtree is: *       Result.node: the largest depth node that is equal to or *                    an ancestor of all the deepest nodes of this subtree. *       Result.dist: the number of nodes in the path from the root *                    of this subtree, to the deepest node in this subtree. */class Result {    TreeNode node;    int dist;    Result(int d, TreeNode n) {        node = n;        dist = d;    }}
```

