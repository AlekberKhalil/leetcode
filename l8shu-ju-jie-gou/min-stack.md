# Min Stack

Design a stack that supports push, pop, top, and retrieving the minimum element in constant time.

* push\(x\) -- Push element x onto stack.
* pop\(\) -- Removes the element on top of the stack.
* top\(\) -- Get the top element.
* getMin\(\) -- Retrieve the minimum element in the stack.

**Example:**

```text
MinStack minStack = new MinStack();minStack.push(-2);minStack.push(0);minStack.push(-3);minStack.getMin();   --> Returns -3.minStack.pop();minStack.top();      --> Returns 0.minStack.getMin();   --> Returns -2.
```

分析

维护2个栈，每次都一起增删，长度一直都一样

```text
class MinStack {    Stack<Integer> s;    Stack<Integer> min;    /** initialize your data structure here. */    public MinStack() {        s = new Stack<Integer>();        min = new Stack<Integer>();    }    public void push(int x) {        s.push(x);        if(min.isEmpty() || min.peek() > x){            min.push(x);        }else{            min.push(min.peek());        }    }    public void pop() {        s.pop();        min.pop();    }    public int top() {        return s.peek();    }    public int getMin() {        return min.peek();    }}/** * Your MinStack object will be instantiated and called as such: * MinStack obj = new MinStack(); * obj.push(x); * obj.pop(); * int param_3 = obj.top(); * int param_4 = obj.getMin(); */
```

