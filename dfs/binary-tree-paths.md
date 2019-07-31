# Binary Tree Paths

Given a binary tree, return all root-to-leaf paths.

For example, given the following binary tree:

```text
   1
 /   \
2     3
 \
  5
```

All root-to-leaf paths are:

```text
["1->2->5", "1->3"]
```

分析

不用stringbuilder 因为正负号和数字长度未知。注意"-&gt;“的位置在最后。

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
    List<String> ret = new ArrayList<>();
    public List<String> binaryTreePaths(TreeNode root) {  
        if(root == null){
            return ret;
        }        
        helper(root, "");
        return ret;
    }
    void helper(TreeNode root, String path){                      
        if(root.left == null && root.right == null){             
            ret.add(path + root.val);           
        }

        if(root.left != null){            
             helper(root.left, path + root.val  + "->");            
        }           
        if(root.right != null){
            helper(root.right, path + root.val + "->");            
        }
    }
}
```

