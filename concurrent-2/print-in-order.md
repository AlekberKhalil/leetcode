# Print in Order

Suppose we have a class:

```text
public class Foo {
  public void first() { print("first"); }
  public void second() { print("second"); }
  public void third() { print("third"); }
}
```

The same instance of `Foo` will be passed to three different threads. Thread A will call `first()`, thread B will call `second()`, and thread C will call `third()`. Design a mechanism and modify the program to ensure that `second()` is executed after `first()`, and `third()` is executed after `second()`.

**Example 1:**

```text
Input: [1,2,3]
Output: "firstsecondthird"
Explanation: There are three threads being fired asynchronously. The input [1,2,3] means thread A calls first(), thread B calls second(), and thread C calls third(). "firstsecondthird" is the correct output.
```

**Example 2:**

```text
Input: [1,3,2]
Output: "firstsecondthird"
Explanation: The input [1,3,2] means thread A calls first(), thread B calls third(), and thread C calls second(). "firstsecondthird" is the correct output.
```

**Note:**

We do not know how the threads will be scheduled in the operating system, even though the numbers in the input seems to imply the ordering. The input format you see is mainly to ensure our tests' comprehensiveness.

分析

semaphore，只有后两个需要semaphore，初始都设置为1，因为不能运行。

```text
import java.util.concurrent.*;
class Foo {
    Semaphore run2;
    Semaphore run3;

    public Foo() {
        run2 = new Semaphore(0);
        run3 = new Semaphore(0);
        
        
    }

    public void first(Runnable printFirst) throws InterruptedException {
        
        // printFirst.run() outputs "first". Do not change or remove this line.
        printFirst.run();
        run2.release();
    }

    public void second(Runnable printSecond) throws InterruptedException {
        run2.acquire();
        // printSecond.run() outputs "second". Do not change or remove this line.
        printSecond.run();
        run3.release();
    }

    public void third(Runnable printThird) throws InterruptedException {
        run3.acquire();
        // printThird.run() outputs "third". Do not change or remove this line.
        printThird.run();
        
    }
}
```

用synchronized, volatile 可不用在这里。好像synchronized 和wait, notifyall一起用？

```text

class Foo {
    private volatile boolean v1;
    private volatile boolean v2;

    public Foo() {
        v1 = false;
        v2 = false;
        
    }

    public synchronized void first(Runnable printFirst) throws InterruptedException {
        
        
        // printFirst.run() outputs "first". Do not change or remove this line.
        printFirst.run();
        v1 = true;
        notifyAll();
        
    }

    public synchronized void second(Runnable printSecond) throws InterruptedException {
       while(!v1){
           wait();
       }
        // printSecond.run() outputs "second". Do not change or remove this line.
        printSecond.run();
        v2 = true;
        notifyAll();
    }

    public synchronized void third(Runnable printThird) throws InterruptedException {
        while(!v2){
            wait();
        }
        // printThird.run() outputs "third". Do not change or remove this line.
        printThird.run();
            
        
    }
}
```



```text
AtomicInteger 3个函数都要判断while
```

```text
import java.util.concurrent.atomic.AtomicInteger;
class Foo {
    AtomicInteger count = new AtomicInteger();
    
    public Foo() {
        count.set(0);
    }

    public void first(Runnable printFirst) throws InterruptedException {
       while (!count.compareAndSet(0,1)){
            
        }
        // printFirst.run() outputs "first". Do not change or remove this line.
        printFirst.run();
        
    }

    public void second(Runnable printSecond) throws InterruptedException {
         while (!count.compareAndSet(1,2)){
            
        }
        // printSecond.run() outputs "second". Do not change or remove this line.
        printSecond.run();
        
    }

    public void third(Runnable printThird) throws InterruptedException {
         while (!count.compareAndSet(2,3)){
          
        }
        // printThird.run() outputs "third". Do not change or remove this line.
        printThird.run();
    }
}
```

