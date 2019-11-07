# Search Range in Binary Search Tree

Given two values k1 and k2 \(where k1 &lt; k2\) and a root pointer to a Binary Search Tree. Find all the keys of tree in range k1 to k2. i.e. print all x such that k1&lt;=x&lt;=k2 and x is a key of given BST. Return all the keys in ascending order.

**Example**

If k1 =`10`and k2 =`22`, then your function should return`[12, 20, 22]`.

```text
    20
   /  \
  8   22
 / \
4   12
```

分析

分治法

```text
    public List<Integer> searchRange(TreeNode root, int k1, int k2) {
        // write your code here
        List<Integer> ret = new ArrayList<Integer>();
        if(root == null)
            return ret;

        List<Integer> left = searchRange(root.left, k1, k2);
        List<Integer> right = searchRange(root.right, k1, k2);
        ret.addAll(left);
        if(root.val >= k1 && root.val <= k2){
            ret.add(root.val);
        }
        ret.addAll(right);
        return ret;
    }
```

