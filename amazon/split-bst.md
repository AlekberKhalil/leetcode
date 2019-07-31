# Split BST

Given a Binary Search Tree \(BST\) with root node`root`, and a target value`V`, split the tree into two subtrees where one subtree has nodes that are all smaller or equal to the target value, while the other subtree has all nodes that are greater than the target value. It's not necessarily the case that the tree contains a node with value`V`.

Additionally, most of the structure of the original tree should remain. Formally, for any child C with parent P in the original tree, if they are both in the same subtree after the split, then node C should still have the parent P.

You should output the root TreeNode of both subtrees after splitting, in any order.

**Example 1:**

```text
Input:
 root = [4,2,6,1,3,5,7], V = 2

Output:
 [[2,1],[4,3,6,null,null,5,7]]

Explanation:

Note that root, output[0], and output[1] are TreeNode objects, not arrays.

The given tree [4,2,6,1,3,5,7] is represented by the following diagram:

          4
        /   \
      2      6
     / \    / \
    1   3  5   7

while the diagrams for the outputs are:

          4
        /   \
      3      6      and    2
            / \           /
           5   7         1
```

**Note:**

1. The size of the BST will not exceed`50`

   .

2. The BST is always valid and each node's value is different.

分析

结果是左右树的root.用递归的话，每次根据root.val和V的大小判断进入哪棵子树继续递归。子树递归的结果也是分成左右树（一大一小）让root指向子树其中一棵子子树，剩下的子子树是另一根。

答案

recursive

```text
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
class Solution {
    public TreeNode[] splitBST(TreeNode root, int V) {
        TreeNode[] ret = new TreeNode[2];
        if(root == null) {
            return new TreeNode[]{null, null};
        }
        if(root.val <= V) {
            ret = splitBST(root.right, V);//这里得到 结果也是2个子树，其中左子树给root做右树，剩下的右树是就是结果右树。
            root.right = ret[0];
            return new TreeNode[]{root, ret[1]};
        } else {
            ret = splitBST(root.left, V);
            root.left = ret[1];
            return new TreeNode[]{ret[0], root};
        }
    }


}
```

iterative

规律是小树总是更新右树，大树总是更新左树

```text
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
class Solution {
    public TreeNode[] splitBST(TreeNode root, int V) {
        TreeNode dummySm = new TreeNode(0);
        TreeNode curSm = dummySm;
        TreeNode dummyLg = new TreeNode(0);
        TreeNode curLg = dummyLg;

        while(root != null) {
            if(root.val <= V) {
                curSm.right = root;
                curSm = root;
                //先把root跳到右树后再把右树置空。右树需要置空否则可能出现一个Node2个parent的情况
                root = root.right;
                curSm.right = null;
            } else {
                curLg.left = root;
                curLg = root;

                root = root.left;
                curLg.left = null;
            }
        }
        return new TreeNode[]{dummySm.right, dummyLg.left};
    }
}
```

