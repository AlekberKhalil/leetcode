# Binary Tree Preorder Traversal

Given a binary tree, return the preorder traversal of its nodes' values.

**Example**

Given:

```text
    1
   / \
  2   3
 / \
4   5
```

return`[1,2,4,5,3]`.

traverse: return void

```text
public class Solution {
    /*
     * @param root: A Tree
     * @return: Preorder in ArrayList which contains node values.
     */
    public List<Integer> preorderTraversal(TreeNode root) {
        // write your code here
        List<Integer> ret = new ArrayList<Integer>();
        if(root == null)
            return ret;
        helper(root, ret);
        return ret;
    }

    public void helper(TreeNode root, List<Integer> ret){
        if(root == null)
            return ;
        ret.add(root.val);
        helper(root.left, ret);
        helper(root.right, ret);
    }
}
```

Divide and conqure

```text
    public List<Integer> preorderTraversal(TreeNode root) {
        // write your code here
        List<Integer> ret = new ArrayList<Integer>();
        if(root == null)
            return ret;

        List<Integer> left = preorderTraversal(root.left);
        List<Integer> right = preorderTraversal(root.right);
        ret.add(root.val);
        ret.addAll(left);
        ret.addAll(right);
        return ret;
    }
```

iterative

preorder是唯一一个while循环里没有cur != null 的，也是唯一一个while循环前先把root加入stack的，所以while只需要判断stack是否为空。

```text
    public List<Integer> preorderTraversal(TreeNode root) {
        // write your code here
        List<Integer> ret = new ArrayList<Integer>();
        if(root == null)
            return ret;
        Stack<TreeNode> s = new Stack<TreeNode>();
        s.push(root);
        while(!s.isEmpty()){
            TreeNode cur = s.pop();
            ret.add(cur.val);
            if(cur.right != null){
                s.push(cur.right);
            }
            if(cur.left != null){
                s.push(cur.left);
            }
        }

        return ret;
    }
```

