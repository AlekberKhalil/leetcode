# Binary Tree Postorder Traversal

Iterative

[http://www.jianshu.com/p/456af5480cee](http://www.jianshu.com/p/456af5480cee)

先走到左子树底，此时此Node已无左子树，看看是否有右子树，没有或者已经visit过，就可以输出了。有的话转入右子树继续遍历。所以需要lastVisited标记。

一直走到左边底端的代码一直错，要注意，直接比较cur和加cur，不是cur.left！

```text
    public List<Integer> postorderTraversal(TreeNode root) {        List<Integer> ret = new ArrayList<Integer>();        if(root == null)        return ret;        Stack<TreeNode> s = new Stack<TreeNode>();        TreeNode cur = root;                TreeNode lastVisit = cur;        while(cur != null || !s.isEmpty()){            while(cur != null){                s.push(cur);                cur = cur.left;            }            cur = s.peek();            //如果右子树不存在或者已经访问，直接输出            if(cur.right == null || cur.right == lastVisit){                s.pop();                ret.add(cur.val);                lastVisit = cur;                cur = null;//此处联想right都遍历过了，无处可去所以cur=null            }else{                cur = cur.right;//否则转入右子树继续            }        }        return ret;    }
```

Recursive

```text
    public List<Integer> postorderTraversal(TreeNode root) {        List<Integer> ret = new ArrayList<Integer>();        if(root == null)        return ret;        List<Integer> left = postorderTraversal(root.left);        List<Integer> right = postorderTraversal(root.right);        ret.addAll(left);        ret.addAll(right);        ret.add(root.val);        return ret;    }
```

另一种解法是使用两个栈。试着在纸上写一下代码。我认为这种解法非常的神奇而优美。你可能觉得这很不可思议，但实际上它做的是反向的先序遍历。亦即遍历的顺序是：节点 -&gt;右子树 -&gt;左子树。这生成的是后根遍历的逆序输出。使用第二个栈，再执行一次反向输出即可得到所要的结果。其实第一个栈就是前序遍历的栈实现，只是先右后左而已，然后栈再倒一次。

C++

```text
void postOrderTraversalIterativeTwoStacks(BinaryTree *root) {     if (!root) return;     stack<BinaryTree*> s;     stack<BinaryTree*> output;     s.push(root);     while (!s.empty())         {             BinaryTree *curr= s.top();             output.push(curr);             s.pop();             if (curr->left) s.push(curr->left);             if (curr->right) s.push(curr->right);         }     while (!output.empty())         {             cout << output.top()->data << " ";            output.pop();        }}
```

