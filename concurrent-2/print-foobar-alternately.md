# Print FooBar Alternately



Suppose you are given the following code:

```text
class FooBar {
  public void foo() {
    for (int i = 0; i < n; i++) {
      print("foo");
    }
  }

  public void bar() {
    for (int i = 0; i < n; i++) {
      print("bar");
    }
  }
}
```

The same instance of `FooBar` will be passed to two different threads. Thread A will call `foo()` while thread B will call `bar()`. Modify the given program to output "foobar" _n_ times.

**Example 1:**

```text
Input: n = 1
Output: "foobar"
Explanation: There are two threads being fired asynchronously. One of them calls foo(), while the other calls bar(). "foobar" is being output 1 time.
```

**Example 2:**

```text
Input: n = 2
Output: "foobarfoobar"
Explanation: "foobar" is being output 2 times.
```

分析

semaphore（nums）nums设置开始几个线程可以访问，所以foo用的那个要为1

```text
import java.util.concurrent.Semaphore;
class FooBar {
    private int n;
    Semaphore s1 = new Semaphore(0);;
    Semaphore s2 = new Semaphore(1);

    public FooBar(int n) {
        this.n = n;
    }

    public void foo(Runnable printFoo) throws InterruptedException {
        
        for (int i = 0; i < n; i++) {
            s2.acquire();
        	// printFoo.run() outputs "foo". Do not change or remove this line.
        	printFoo.run();
            s1.release();
        }
    }

    public void bar(Runnable printBar) throws InterruptedException {
        
        for (int i = 0; i < n; i++) {
            s1.acquire();
            // printBar.run() outputs "bar". Do not change or remove this line.
        	printBar.run();
            s2.release();
        }
    }
}
```

