# My Calendar I



Implement a `MyCalendar` class to store your events. A new event can be added if adding the event will not cause a double booking.

Your class will have the method, `book(int start, int end)`. Formally, this represents a booking on the half open interval `[start, end)`, the range of real numbers `x` such that `start <= x < end`.

A double booking happens when two events have some non-empty intersection \(ie., there is some time that is common to both events.\)

For each call to the method `MyCalendar.book`, return `true` if the event can be added to the calendar successfully without causing a double booking. Otherwise, return `false` and do not add the event to the calendar.Your class will be called like this: `MyCalendar cal = new MyCalendar();` `MyCalendar.book(start, end)`

**Example 1:**

```text
MyCalendar();
MyCalendar.book(10, 20); // returns true
MyCalendar.book(15, 25); // returns false
MyCalendar.book(20, 30); // returns true
Explanation: 
The first event can be booked.  The second can't because time 15 is already booked by another event.
The third event can be booked, as the first event takes every time less than 20, but not including 20.
```

**Note:**

* The number of calls to `MyCalendar.book` per test case will be at most `1000`.
* In calls to `MyCalendar.book(start, end)`, `start` and `end` are integers in the range `[0, 10^9]`.

分析

用BST做，加入 Node 的規則是: If curr node.start &gt;= new event.end, go left If curr node.end &lt;= new event.start, go right no way out, so there is a conflict

```text
class Node:
    def __init__(self,s,e):        
        self.s = s
        self.e = e
        self.left = None
        self.right = None
    
class MyCalendar:

    def __init__(self):
        self.root = None
        
    def helper(self, s: int, e: int, node: Node)->bool:
        if s >= node.e:
            if node.right:
                return self.helper(s,e,node.right)                
            else:
                node.right = Node(s,e)
                return True
        elif e <= node.s:
            if node.left:
                return self.helper(s,e,node.left)                
            else:
                node.left = Node(s,e)
                return True
        else:
            return False
        
    def book(self, start: int, end: int) -> bool:
        if not self.root:
            self.root = Node(start,end)
            return True
        return self.helper(start,end,self.root)
        


# Your MyCalendar object will be instantiated and called as such:
# obj = MyCalendar()
# param_1 = obj.book(start,end)
```

初始化必须treeset。 lambda多参数要括号

```text
class MyCalendar {
    TreeSet<int[]> books;//必须要treeset 不能只set

    public MyCalendar() {
        books = new TreeSet<>((int[] a, int[] b) -> a[0] - b[0]);//前面参数要（）
    }
    
    public boolean book(int start, int end) {
        int[] book = new int[] {start,end}, floor = books.floor(book), ceiling = books.ceiling(book);
        if(floor != null && floor[1] > start)//不能 = 因为题目不含end
            
            return false;
        if(ceiling != null && ceiling[0] < end)
            return false;
        books.add(book);
        return true;
    }
}

/**
 * Your MyCalendar object will be instantiated and called as such:
 * MyCalendar obj = new MyCalendar();
 * boolean param_1 = obj.book(start,end);
 */
```

python 模仿treeset， 维持有序数组。每次取前个数和后个数start end 比较。

```text
class MyCalendar:

    def __init__(self):
        self.arr = []
        

    def book(self, start: int, end: int) -> bool:
        idx = bisect.bisect_left(self.arr,(start,end))
        left_valid = idx == 0 or self.arr[idx-1][1] <= start
        right_valid = idx == len(self.arr) or end <= self.arr[idx][0] >= end #注意不是Idx+1
        if left_valid and right_valid:
            self.arr.insert(idx,(start,end))
            return True
        
        return False
        

        


# Your MyCalendar object will be instantiated and called as such:
# obj = MyCalendar()
# param_1 = obj.book(start,end)
```

还可以建binary tree, 每次插入左右边或者递归。能插入就True。不能就false。



