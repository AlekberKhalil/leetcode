# Flatten Nested List Iterator\(DFS,Iter\)

Given a nested list of integers, implement an iterator to flatten it.

Each element is either an integer, or a list -- whose elements may also be integers or other lists.

**Example 1:**

```text
Input: [[1,1],2,[1,1]]Output: [1,1,2,1,1]Explanation: By calling next repeatedly until hasNext returns false,              the order of elements returned by next should be: [1,1,2,1,1].
```

**Example 2:**

```text
Input: [1,[4,[6]]]Output: [1,4,6]Explanation: By calling next repeatedly until hasNext returns false,              the order of elements returned by next should be: [1,4,6].
```

分析：

python 强大的for loop来做dfs

```text
# """# This is the interface that allows for creating nested lists.# You should not implement it, or speculate about its implementation# """#class NestedInteger(object):#    def isInteger(self):#        """#        @return True if this NestedInteger holds a single integer, rather than a nested list.#        :rtype bool#        """##    def getInteger(self):#        """#        @return the single integer that this NestedInteger holds, if it holds a single integer#        Return None if this NestedInteger holds a nested list#        :rtype int#        """##    def getList(self):#        """#        @return the nested list that this NestedInteger holds, if it holds a nested list#        Return None if this NestedInteger holds a single integer#        :rtype List[NestedInteger]#        """class NestedIterator(object):    def dfs(self,node):        if node.isInteger():            return [node.getInteger()]        return [item for child in node.getList() for item in self.dfs(child)]    def __init__(self, nestedList):        """        Initialize your data structure here.        :type nestedList: List[NestedInteger]        """        self.arr = [item for child in nestedList for item in self.dfs(child)]        self.pos = 0        self.N = len(self.arr)    def next(self):        """        :rtype: int        """        if self.hasNext():            self.pos += 1            return self.arr[self.pos-1]        else:            return -1    def hasNext(self):        """        :rtype: bool        """        if self.pos >= self.N:            return False        return True# Your NestedIterator object will be instantiated and called as such:# i, v = NestedIterator(nestedList), []# while i.hasNext(): v.append(i.next())
```

用stack+iter做

栈里赛的都是Iter

has next 每次看栈顶元素，没有next就是当前list空了，弹出，有元素是int直接返回true，有元素是List，把list iter塞入stack

```text
# """# This is the interface that allows for creating nested lists.# You should not implement it, or speculate about its implementation# """# class NestedInteger(object):#    def isInteger(self):#        """#        @return True if this NestedInteger holds a single integer, rather than a nested list.#        :rtype bool#        """##    def getInteger(self):#        """#        @return the single integer that this NestedInteger holds, if it holds a single integer#        Return None if this NestedInteger holds a nested list#        :rtype int#        """##    def getList(self):#        """#        @return the nested list that this NestedInteger holds, if it holds a nested list#        Return None if this NestedInteger holds a single integer#        :rtype List[NestedInteger]#        """class NestedIterator(object):    def __init__(self, nestedList):        """        Initialize your data structure here.        :type nestedList: List[NestedInteger]        """        self.stack = [iter(nestedList)]        self.nxt = None        self.defval = -1    def next(self):        """        :rtype: int        """        return self.nxt.getInteger() if self.nxt else None    def hasNext(self):        """        :rtype: bool        """        while self.stack:            self.nxt = next(self.stack[-1], self.defval)            if self.nxt == self.defval:                self.stack.pop()            elif self.nxt.isInteger():                return True            else:                self.stack.append(iter(self.nxt.getList()))        return False# Your NestedIterator object will be instantiated and called as such:# i, v = NestedIterator(nestedList), []# while i.hasNext(): v.append(i.next())
```

