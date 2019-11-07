# Implement Queue by Two Stacks

As the title described, you should only use two stacks to implement a queue's actions.

The queue should support`push(element)`,`pop()`and`top()`where pop is pop the first\(a.k.a front\) element in the queue.

Both pop and top methods should return the value of first element.

**Example**

```text
push(1)
pop()     // return 1
push(2)
push(3)
top()     // return 2
pop()     // return 2
```

分析

一个栈进，一个栈出，每次pop或者top时候，若s2空，s1都倒入s2

```text
public class MyQueue {
    private Stack<Integer> stack1;
    private Stack<Integer> stack2;
    public MyQueue() {
        // do intialization if necessary
        stack1 = new Stack<Integer>();
        stack2 = new Stack<Integer>();
    }

    /*
     * @param element: An integer
     * @return: nothing
     */
    public void push(int element) {
        // write your code here
        stack1.push(element);
    }

    /*
     * @return: An integer
     */
    public int pop() {
        // write your code here
        if(!stack2.isEmpty()){
            return stack2.pop();
        }else{
            while(!stack1.isEmpty()){
                stack2.push(stack1.pop());
            }
        }
        return stack2.pop();
    }

    /*
     * @return: An integer
     */
    public int top() {
        // write your code here
        if(!stack2.isEmpty()){
            return stack2.peek();
        }else{
            while(!stack1.isEmpty()){
                stack2.push(stack1.pop());
            }
        }
        return stack2.peek();
    }
}
```

