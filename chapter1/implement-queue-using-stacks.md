# Implement Queue using Stacks

Implement the following operations of a queue using stacks.

* push\(x\) -- Push element x to the back of queue.
* pop\(\) -- Removes the element from in front of queue.
* peek\(\) -- Get the front element.
* empty\(\) -- Return whether the queue is empty.

分析：

in栈只进，out栈只出。out空了从In导入

```text
class MyQueue {    Stack<Integer> in, out;    /** Initialize your data structure here. */    public MyQueue() {        in = new Stack<Integer>();        out = new Stack<Integer>();    }    /** Push element x to the back of queue. */    public void push(int x) {        in.push(x);    }    /** Removes the element from in front of queue and returns that element. */    public int pop() {        if(out.empty()){            while(!in.empty()){                out.push(in.pop());            }        }        return out.pop();    }    /** Get the front element. */    public int peek() {        if(out.empty()){            while(!in.empty()){                out.push(in.pop());            }        }        return out.peek();    }    /** Returns whether the queue is empty. */    public boolean empty() {        return in.empty() && out.empty();    }}/** * Your MyQueue object will be instantiated and called as such: * MyQueue obj = new MyQueue(); * obj.push(x); * int param_2 = obj.pop(); * int param_3 = obj.peek(); * boolean param_4 = obj.empty(); */
```

