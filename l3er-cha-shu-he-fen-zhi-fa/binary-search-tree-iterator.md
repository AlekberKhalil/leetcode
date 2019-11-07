# Binary Search Tree Iterator

Implement an iterator over a binary search tree \(BST\). Your iterator will be initialized with the root node of a BST.

Calling`next()`will return the next smallest number in the BST.

**Note:**`next()`and`hasNext()`should run in average O\(1\) time and uses O\(h\) memory, wherehis the height of the tree.

分析

就是inorder的while遍历拆成2部分。

```text
public class BSTIterator {    private TreeNode next;    private Stack<TreeNode> s = new Stack<TreeNode>();    private void addToStack(){        while(next != null){            s.add(next);            next = next.left;        }        next = null;    }    public BSTIterator(TreeNode root) {        next = root;    }    /** @return whether we have a next smallest number */    public boolean hasNext() {        if(next != null){            addToStack();        }        return !s.isEmpty();    }    /** @return the next smallest number */    public int next() {        if(!hasNext()){            return -1;        }        next = s.pop();        int ret = next.val;        next = next.right;        return ret;    }}
```

不用额外函数的做法

二刷错误：1.忘了用栈 2. hasNext里的while写错了，root不空的话，先推入栈再转左。

```text
/** * Definition for binary tree * public class TreeNode { *     int val; *     TreeNode left; *     TreeNode right; *     TreeNode(int x) { val = x; } * } */public class BSTIterator {    TreeNode cur;    Stack<TreeNode> s = new Stack<TreeNode>();    public BSTIterator(TreeNode root) {        cur = root;    }    /** @return whether we have a next smallest number */    public boolean hasNext() {                while(cur != null){            s.push(cur);            cur = cur.left;        }        return !s.isEmpty();    }    /** @return the next smallest number */    public int next() {        if(!s.isEmpty()){            cur = s.pop();             int ret = cur.val;            cur = cur.right;            return ret;        }        return -1;    }}/** * Your BSTIterator will be called like this: * BSTIterator i = new BSTIterator(root); * while (i.hasNext()) v[f()] = i.next(); */
```

