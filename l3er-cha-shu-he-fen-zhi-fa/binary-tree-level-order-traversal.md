# Binary Tree Level Order Traversal\(dfs,bfs,python\)

Given a binary tree, return thelevel ordertraversal of its nodes' values. \(ie, from left to right, level by level\).

For example:  
Given binary tree`[3,9,20,null,null,15,7]`,

```text
    3
   / \
  9  20
    /  \
   15   7
```

return its level order traversal as:

```text
[
  [3],
  [9,20],
  [15,7]
]
```

分析

bfs， q size一直在变，所以开始就要提取出来做for loop

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
    public List<List<Integer>> levelOrder(TreeNode root) {
        List<List<Integer>> ret = new ArrayList<>();
        if(root == null)
            return ret;

        bfs(root, ret);
            return ret;
    }

    public void bfs(TreeNode root, List<List<Integer>> ret){
        Queue<TreeNode> q = new LinkedList<TreeNode>();
        q.offer(root);
        while(!q.isEmpty()){
            List<Integer> level = new ArrayList<Integer>();
            int size = q.size();
            for(int i = 0; i < size; i ++){
                TreeNode cur = q.poll();
                level.add(cur.val);
                if(cur.left != null){
                    q.offer(cur.left);
                }
                if(cur.right != null){
                    q.offer(cur.right);
                }
            }
            ret.add(level);
        }        
    }
}
```

```text
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution(object):
    def levelOrder(self, root):
        """
        :type root: TreeNode
        :rtype: List[List[int]]
        """
        ret = []
        if not root:
            return ret
        q = [root]
        while q:
            path = []
            n = len(q)
            for i in range(n):
                cur = q.pop(0)
                path.append(cur.val)
                if cur.left:
                    q.append(cur.left)
                if cur.right:
                    q.append(cur.right)
            ret.append(path)
        return ret
```

dfs

利用height，每次height&lt;len\(res\),就加一个array

```text
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution(object):
    def levelOrder(self, root):
        """
        :type root: TreeNode
        :rtype: List[List[int]]
        """

        ret = []
        if not root:
            return ret
        self.dfs(root,ret,1)
        return ret

    def dfs(self,root,ret,height):
        if height > len(ret):
            ret.append([])
        ret[height-1].append(root.val)
        if root.left:
            self.dfs(root.left,ret,height+1)
        if root.right:
            self.dfs(root.right, ret, height + 1)
```

