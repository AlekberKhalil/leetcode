# Binary Tree Inorder Traversal

Iterative

在进入while循环之前什么都不做，先把cur=root。进去之后，首先再用一个wihle一直往左走知道尽头，也一路的存入stack，然后把顶元素存入result，并且这时候把cur变成顶元素的右儿子。

想象cur从root初始开始打怪兽。stack为空不加入root。在while里cur一路给stack充值直到cur空，然后stack pop给cur值，然后cur到right 继续。

注意此处while条件是or

```text
public List<Integer> inorderTraversal(TreeNode root) {        List<Integer> ret = new ArrayList<Integer>();        if(root == null)            return ret;        Stack<TreeNode> s = new Stack<TreeNode>();        TreeNode cur = root;        while(cur != null || !s.isEmpty()){            while(cur != null){                s.push(cur);                cur = cur.left;            }            cur = s.pop();            ret.add(cur.val);            cur = cur.right;        }        return ret;    }
```

Recursive

```text
    public List<Integer> inorderTraversal(TreeNode root) {        List<Integer> ret = new ArrayList<Integer>();        if(root == null)            return ret;        List<Integer> left = inorderTraversal(root.left);        List<Integer> right = inorderTraversal(root.right);        ret.addAll(left);        ret.add(root.val);        ret.addAll(right);        return ret;    }
```

