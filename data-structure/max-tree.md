# Max Tree

## Question <a id="question"></a>

Given an integer array with no duplicates. A max tree building on this array is defined as follow:

The root is the maximum number in the array The left subtree and right subtree are the max trees of the subarray divided by the root number. Construct the max tree by the given array.

Example Given`[2, 5, 6, 0, 3, 1]`, the max tree constructed by this array is:

```text
    6
   / \
  5   3
 /   / \
2   0   1
```

Challenge`O(n)`time and memory.

## Thoughts <a id="thoughts"></a>

采用up-down的方法就是recursive call

采用Bottom-up

loop through the array, 建立一个stack, 对于每一个elment nums\[i\]

1. if nums\[i\] &gt; stack\[-1\], 要找到stack里比nums\[i\]小的最近的最大值， 所以一直pop并且nums\[i\].left = stack.pop\(\)
2. 直到nums\[i\] &lt; stack\[-1\], 这时stack的顶top是比nums\[i\]大的左边的第一个值，nums\[i\]先设为它的right child\(如果之后有值在top和nums\[i\]之间，会因为第一步被更新，它会一直指向最新nums\[i\]如果需要的话\)
3. 将nums\[i\] push到stack上
4. 最终return stack的第一个

大沉底小出去。for loop所有数，栈内所有比它小的数弹出，大数留着。压入栈时候就是算好了左值的，因为根据已有信息已经能算左值了，新来数时栈内大数都会试探性赋右值。

## Solution <a id="solution"></a>

recursive版本

```text
public class Solution {
    //recursive
    public TreeNode constructMaximumBinaryTree(int[] nums) {
        return helper(nums, 0, nums.length-1);
    }
    public TreeNode helper(int[] nums, int left, int right){
        if(left > right)
            return null;
        int maxPos = left;
        for(int i = left+1; i <= right; i++){
            if(nums[maxPos] < nums[i]){
                maxPos = i;
            }
        }

        TreeNode root = new TreeNode(nums[maxPos]);
        root.left = helper(nums, left, maxPos-1);
        root.right = helper(nums, maxPos+1, right);
        return root;
    }
}
```

```java
public class Solution {
    public TreeNode constructMaximumBinaryTree(int[] nums) {
        Stack<TreeNode> s = new Stack<TreeNode>();
        for(int n : nums){
            TreeNode node = new TreeNode(n);
            while(!s.empty() && s.peek().val <= n){
                node.left = s.pop(); //一直pop到左边最远比它小
            }
            if(!s.empty())
                s.peek().right = node;//下一个就比它大了
            s.push(node); //无论如何加入栈内
        }

        TreeNode ret = s.pop();
        while(!s.empty()) {
            ret = s.pop();//是弹出第一个元素，最大那个
        }
        return ret;
    }
}
```

