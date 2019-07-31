# Serialize and Deserialize Binary Tree\(bfs&dfs\)

Serialization is the process of converting a data structure or object into a sequence of bits so that it can be stored in a file or memory buffer, or transmitted across a network connection link to be reconstructed later in the same or another computer environment.

Design an algorithm to serialize and deserialize a binary tree. There is no restriction on how your serialization/deserialization algorithm should work. You just need to ensure that a binary tree can be serialized to a string and this string can be deserialized to the original tree structure.

**Example:** 

```text
You may serialize the following tree:

    1
   / \
  2   3
     / \
    4   5

as 
"[1,2,3,null,null,4,5]"
```

**Clarification:**The above format is the same as[how LeetCode serializes a binary tree](https://leetcode.com/faq/#binary-tree). You do not necessarily need to follow this format, so please be creative and come up with different approaches yourself.

**Note:** Do not use class member/global/static variables to store states. Your serialize and deserialize algorithms should be stateless.

分析

serialize 就是pre order遍历

deserialize就是顺序按照i, 2i+1,2i+2来拼装树。

第一遍以为是level order遍历，居然也过了,好像就是level order的

其实正确string是：\[1,2,null,null,3,4,null,null,5,null,null\]

BFS

```text
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Codec:

    def serialize(self, root):
        """Encodes a tree to a single string.

        :type root: TreeNode
        :rtype: str
        """
        if not root:
            return ""
        ret = []
        q = [root]
        while q:
            size = len(q)
            for i in range(size):
                cur = q.pop(0)

                if cur:
                    ret.append(str(cur.val))
                    q.append(cur.left)
                    q.append(cur.right)
                else:
                    ret.append('null')

        return '['+','.join(ret)+']'

    def deserialize(self, data):
        """Decodes your encoded data to tree.

        :type data: str
        :rtype: TreeNode
        """
        # [1, 2, 3, null, null, 4, 5]
        if not data or len(data)==0:
            return None

        data = data[1:-1].split(',')
        llen = len(data)
        root = TreeNode(int(data[0]))
        q = [root]
        i = 1
        while i < llen and q:
            node = q.pop(0)
            if data[i] != 'null':
                node.left = TreeNode(int(data[i]))
                q.append(node.left)
            i+=1#都要+1跳过左树，下同

            if i <llen and data[i] != 'null':

                node.right = TreeNode(int(data[i]))
                q.append(node.right)
            i += 1

        return root
# Your Codec object will be instantiated and called as such:
# codec = Codec()
# root = codec.deserialize("[1,2,3,null,null,4,5]")
# ret = codec.serialize(root)
# print(ret)
```

第二遍 preorder dfs

pos作为参数传入 pos+=1始终没用，最后用list.pop\(0\)才解决

```text
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Codec:
    def buildString(self,root,path):
        if not root:
            path.append('X') #空node用X
        else:
            path.append(str(root.val))
            self.buildString(root.left,path)
            self.buildString(root.right,path)


    def serialize(self, root):
        """Encodes a tree to a single string.

        :type root: TreeNode
        :rtype: str
        """
        path =[]
        self.buildString(root,path)
        return ' '.join(path)

    def deserialize(self, data):
        """Decodes your encoded data to tree.

        :type data: str
        :rtype: TreeNode
        """
        data = data.split(' ') #还是要加splitter
        return self.buildTree(data)

    def buildTree(self,data):
        val = data.pop(0)
        if val=='X':
            return None
        root = TreeNode(int(val))

        root.left = self.buildTree(data)
        root.right = self.buildTree(data)
        return root


# Your Codec object will be instantiated and called as such:
# codec = Codec()
# codec.deserialize(codec.serialize(root))
```

preorder Bfs

用q来存root, left,right弹入弹出。data的val用来for loop every item。

直接建好所有Node和Nonelist, 2个list ，一个for loop，一个用来pop。

```text
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Codec:

    def serialize(self, root):
        """Encodes a tree to a single string.

        :type root: TreeNode
        :rtype: str
        """
        if not root:
            return ""
        res = []
        q = [root]
        while q:
            cur = q.pop(0)
            if not cur:
                res.append('x')
            else:
                res.append(str(cur.val))
                q.append(cur.left)
                q.append(cur.right)
        return ' '.join(res)

    def deserialize(self, data):
        """Decodes your encoded data to tree.

        :type data: str
        :rtype: TreeNode
        """
        if data == "":
            return None
        data = data.split(' ')
        # nodes = [TreeNode(int(i)) if i!='x' else None for i in data ]
        # q=nodes[:]
        # root = q.pop(0)
        #
        # for n in nodes:
        #     if q:
        #         n.left =q.pop(0)
        #         n.right = q.pop(0)
        root = TreeNode(data[0])
        q = [root]
        i,n = 1,len(data)
        while i < n:
            cur = q.pop(0)
            if data[i] != 'x':
                cur.left = TreeNode(int(data[i]))
                q.append(cur.left)
            i += 1
            if data[i] !='x':
                cur.right = TreeNode(int(data[i]))
                q.append(cur.right)
            i += 1
        return root



# Your Codec object will be instantiated and called as such:
# codec = Codec()
# codec.deserialize(codec.serialize(root))
```

preorder dfs

```text
class Codec:
    def buildString(self,root,path):
        if not root:
            path.append('X') #空node用X
        else:
            path.append(str(root.val))
            self.buildString(root.left,path)
            self.buildString(root.right,path)


    def serialize(self, root):
        """Encodes a tree to a single string.

        :type root: TreeNode
        :rtype: str
        """
        path =[]
        self.buildString(root,path)
        return ' '.join(path)

    def deserialize(self, data):
        """Decodes your encoded data to tree.

        :type data: str
        :rtype: TreeNode
        """
        data = data.split(' ') #还是要加splitter
        return self.buildTree(data)

    def buildTree(self,data):
        val = data.pop(0)
        if val=='X':
            return None
        root = TreeNode(int(val))

        root.left = self.buildTree(data)
        root.right = self.buildTree(data)
        return root
```

