# Binary Tree Right Side View（FB）

Given a binary tree, imagine yourself standing on therightside of it, return the values of the nodes you can see ordered from top to bottom.

For example:  
Given the following binary tree,

```text
   1            <--- /   \2     3         <--- \     \  5     4       <---
```

You should return`[1, 3, 4]`.

分析

判断每层用那个值，有右值用右值，没有的话用左值。用i == ret.size\(\)。记得先右后左的递归。

```text
/** * Definition for a binary tree node. * public class TreeNode { *     int val; *     TreeNode left; *     TreeNode right; *     TreeNode(int x) { val = x; } * } */class Solution {    List<Integer> ret = new ArrayList<>();    public List<Integer> rightSideView(TreeNode root) {                if(root == null){            return ret;        }        helper(root, 0);        return ret;    }    void helper(TreeNode root, int i){        if(i == ret.size()){            ret.add(root.val);        }        if(root.right != null){            helper(root.right, i + 1);        }        if(root.left != null){            helper(root.left, i + 1);                   }    }}
```

bfs and dfs

```text
/** * Definition for a binary tree node. * public class TreeNode { *     int val; *     TreeNode left; *     TreeNode right; *     TreeNode(int x) { val = x; } * } */class Solution {    // public List<Integer> rightSideView(TreeNode root) {//BFS注意模板//         Queue<TreeNode> q = new LinkedList<>();//         List<Integer> ret = new ArrayList<>();//         if(root == null){//             return ret;//         }//         q.offer(root);//         while(!q.isEmpty()) {//             List<TreeNode> level = new ArrayList<>();//             int size = q.size();//             for(int i = 0; i < size; i ++) {//                 TreeNode node = q.poll();//                 level.add(node);//                 if(node.right != null)//                     q.offer(node.right);//                 if(node.left != null)//                     q.offer(node.left);//             }//             ret.add(level.get(0).val);//         }//         return ret;    // }    public List<Integer> rightSideView(TreeNode root) {        List<Integer> ret = new ArrayList<>();        helper(root, ret, 0);        return ret;    }    void helper(TreeNode root, List<Integer> ret, int depth) {        if(root == null){            return ;        }        if(depth == ret.size()) {            ret.add(root.val);        }        helper(root.right, ret, depth + 1);        helper(root.left, ret, depth + 1);    }}
```

