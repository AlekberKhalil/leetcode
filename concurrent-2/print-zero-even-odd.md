# Print Zero Even Odd



Suppose you are given the following code:

```text
class ZeroEvenOdd {
  public ZeroEvenOdd(int n) { ... }      // constructor
  public void zero(printNumber) { ... }  // only output 0's
  public void even(printNumber) { ... }  // only output even numbers
  public void odd(printNumber) { ... }   // only output odd numbers
}
```

The same instance of `ZeroEvenOdd` will be passed to three different threads:

1. Thread A will call `zero()` which should only output 0's.
2. Thread B will call `even()` which should only ouput even numbers.
3. Thread C will call `odd()` which should only output odd numbers.

Each of the thread is given a `printNumber` method to output an integer. Modify the given program to output the series `010203040506`... where the length of the series must be 2_n_.

**Example 1:**

```text
Input: n = 2
Output: "0102"
Explanation: There are three threads being fired asynchronously. One of them calls zero(), the other calls even(), and the last one calls odd(). "0102" is the correct output.
```

**Example 2:**

```text
Input: n = 5
Output: "0102030405"
```

分析

因为需要循环打印，所以需要loop，否则只打印一次。

Semaphore 

0的loop里决定释放s1 还是s2. 1,2里都有loop，注意分别是从1,2开始，i+=2

```text
import java.util.concurrent.*;
class ZeroEvenOdd {
    private int n;
    Semaphore s0,s1,s2;
    
    public ZeroEvenOdd(int n) {
        this.n = n;
        this.s0 = new Semaphore(1);
        this.s1 = new Semaphore(0);
        this.s2 = new Semaphore(0);
        
            
    }

    // printNumber.accept(x) outputs "x", where x is an integer.
    public void zero(IntConsumer printNumber) throws InterruptedException {
        
        for(int i = 0; i< n; i ++){
            s0.acquire();
            printNumber.accept(0);
            (i%2 == 0 ? s1 : s2).release();
        }
        
        
    }

    public void even(IntConsumer printNumber) throws InterruptedException {
        for(int i = 2; i<= n; i +=2){
            s2.acquire();
            printNumber.accept(i);
            s0.release();
        }
        
    }

    public void odd(IntConsumer printNumber) throws InterruptedException {
        for(int i = 1; i<= n; i +=2){
            s1.acquire();
            printNumber.accept(i);
            s0.release();
        }
        
    }
}
```

用synchronized。 int signal,记得也是在0的loop里决定sig =1 还是2,。

```text
class ZeroEvenOdd {
    private int n;
    private int sig;
    
    public ZeroEvenOdd(int n) {
        this.n = n;
        this.sig = 0;
    }

    // printNumber.accept(x) outputs "x", where x is an integer.
    public synchronized void zero(IntConsumer printNumber) throws InterruptedException {
        for(int  i = 0; i < n; i ++){
            while(sig != 0){
                wait();
            }
            
            printNumber.accept(sig);
            sig = i %2 == 0 ? 1 : 2;
            notifyAll();
        }
        
    }

    public synchronized void even(IntConsumer printNumber) throws InterruptedException {
        for(int  i = 2; i <= n; i +=2){
             while(sig != 2){
                wait();
            }
            
           printNumber.accept(i);
            sig = 0;
            notifyAll();
            }
       
        
    }

    public synchronized void odd(IntConsumer printNumber) throws InterruptedException {
         for(int  i = 1; i <= n; i +=2){
            while(sig != 1){
                wait();
            }
          
            printNumber.accept(i);
             sig = 0;
            notifyAll();
             }

    }
}
```

