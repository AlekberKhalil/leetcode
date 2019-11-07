# Binary Tree Maximum Path Sum II

## Question <a id="question"></a>

Given a binary tree, find the maximum path sum from root.

The path may end at any node in the tree and contain at least one node in it.

Example

Given the below binary tree:

1 /  2 3

return 4. \(1-&gt;3\)

## 分析 <a id="solution"></a>

唯一要注意的是题目要求至少有一个点，所以左右值先和0比较后再和root值相加。

```text
    public int maxPathSum2(TreeNode root) {        if(root == null)            return 0;        int left = maxPathSum2(root.left);        int right = maxPathSum2(root.right);        return root.val + Math.max(0, Math.max(left, right));    }
```

