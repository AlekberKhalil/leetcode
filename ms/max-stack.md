# Max Stack



Design a max stack that supports push, pop, top, peekMax and popMax.

1. push\(x\) -- Push element x onto stack.
2. pop\(\) -- Remove the element on top of the stack and return it.
3. top\(\) -- Get the element on the top.
4. peekMax\(\) -- Retrieve the maximum element in the stack.
5. popMax\(\) -- Retrieve the maximum element in the stack, and remove it. If you find more than one maximum elements, only remove the top-most one.

**Example 1:**  


```text
MaxStack stack = new MaxStack();
stack.push(5); 
stack.push(1);
stack.push(5);
stack.top(); -> 5
stack.popMax(); -> 5
stack.top(); -> 1
stack.peekMax(); -> 5
stack.pop(); -> 1
stack.top(); -> 5
```

分析

2个stack, 普通和Max stack，一起增和减，大小一样

记得popMax时候 需要把stack里的最大数去掉，需要一个buffer

也可以用LRU做法，double linked list and tree map

```text
class MaxStack:

    def __init__(self):
        """
        initialize your data structure here.
        """
        self.s = []
        self.ms = []
        
        

    def push(self, x: int) -> None:
        self.s.append(x)
        if not self.ms:
            self.ms.append(x)
        else:
            self.ms.append(max(x,self.ms[-1]))
        

    def pop(self) -> int:
        if self.ms:
            self.ms.pop()
        return self.s.pop()
        
        

    def top(self) -> int:
        return self.s[-1]
        

    def peekMax(self) -> int:
        
        return self.ms[-1]
        

    def popMax(self) -> int:        
        mx = self.peekMax()
        buffer = []
        
        while mx != self.s[-1]:
            buffer.append(self.pop())
        self.pop()
        while buffer:
            self.push(buffer.pop())
        
        return mx
        


# Your MaxStack object will be instantiated and called as such:
# obj = MaxStack()
# obj.push(x)
# param_2 = obj.pop()
# param_3 = obj.top()
# param_4 = obj.peekMax()
# param_5 = obj.popMax()
```

