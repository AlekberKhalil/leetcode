# Design Phone Directory



Design a Phone Directory which supports the following operations:

1. `get`: Provide a number which is not assigned to anyone.
2. `check`: Check if a number is available or not.
3. `release`: Recycle or release a number.

**Example:**

```text
// Init a phone directory containing a total of 3 numbers: 0, 1, and 2.PhoneDirectory directory = new PhoneDirectory(3);// It can return any available phone number. Here we assume it returns 0.directory.get();// Assume it returns 1.directory.get();// The number 2 is available, so return true.directory.check(2);// It returns 2, the only number that is left.directory.get();// The number 2 is no longer available, so return false.directory.check(2);// Release number 2 back to the pool.directory.release(2);// Number 2 is available again, return true.directory.check(2);
```



分析

1 一个set放released,  一个int记录当前已达数字（++--）

2 一个set装满所有available，加加减减.cons 初始要O\(N\)

3  java BitSet 和 index。 index就是当前数，release  就clear and set index. get 就 return index and set index

4 segment tree

{% embed url="https://leetcode.com/problems/design-phone-directory/discuss/85342/Python-segment-tree-implementation" %}

{% embed url="https://leetcode.com/problems/design-phone-directory/discuss/119330/My-segment-tree-solution" %}

方法1:

release要有判断，max不可达

```text
class PhoneDirectory:    def __init__(self, maxNumbers: int):        """        Initialize your data structure here        @param maxNumbers - The maximum numbers that can be stored in the phone directory.        """        self.next = 0        self.released = set()        self.max = maxNumbers            def get(self) -> int:        """        Provide a number which is not assigned to anyone.        @return - Return an available number. Return -1 if none is available.        """        res = 0        if self.next < self.max:            res = self.next            self.next += 1            return res        if self.released:            return self.released.pop()                return -1                                def check(self, number: int) -> bool:        """        Check if a number is available or not.        """        if number in self.released or self.next <= number < self.max :            return True        return False            def release(self, number: int) -> None:        """        Recycle or release a number.        """        if number < self.next: #记得要判断这里，而且不是<max            self.released.add(number)        # Your PhoneDirectory object will be instantiated and called as such:# obj = PhoneDirectory(maxNumbers)# param_1 = obj.get()# param_2 = obj.check(number)# obj.release(number)
```

方法2：

```text
class PhoneDirectory:    def __init__(self, maxNumbers: int):        """        Initialize your data structure here        @param maxNumbers - The maximum numbers that can be stored in the phone directory.        """        self.avail = set(range(maxNumbers))            def get(self) -> int:        """        Provide a number which is not assigned to anyone.        @return - Return an available number. Return -1 if none is available.        """        if self.avail:            return self.avail.pop()        return -1            def check(self, number: int) -> bool:        """        Check if a number is available or not.        """        return number in self.avail            def release(self, number: int) -> None:        """        Recycle or release a number.        """        self.avail.add(number)                    # Your PhoneDirectory object will be instantiated and called as such:# obj = PhoneDirectory(maxNumbers)# param_1 = obj.get()# param_2 = obj.check(number)# obj.release(number)
```

3 bitset

Space is much efficient: O\(c\), wouldn’t say it is O\(1\) because we still need max\_size number of bits

这里bit的长度 = max number,某个数字就是设置这个位上的bit

nextClearBit\(num\)注意此处需要参数

```text
class PhoneDirectory {    /** Initialize your data structure here        @param maxNumbers - The maximum numbers that can be stored in the phone directory. */    BitSet bs;    final int max;    int nextAvail;    public PhoneDirectory(int maxNumbers) {        bs = new BitSet(maxNumbers);        max = maxNumbers;        nextAvail = 0;          }        /** Provide a number which is not assigned to anyone.        @return - Return an available number. Return -1 if none is available. */    public int get() {        if (nextAvail >= max) {            return -1;        }        int res = nextAvail;        bs.set(res);         nextAvail = bs.nextClearBit(res);//注意nextClearBit用法，需要传入num        return res;                    }        /** Check if a number is available or not. */    public boolean check(int number) {        return number < max &&  !bs.get(number);            }        /** Recycle or release a number. */    public void release(int number) {        if(number >= 0 && number < max){            bs.clear(number);        }        nextAvail = Math.min(number,nextAvail);            }}/** * Your PhoneDirectory object will be instantiated and called as such: * PhoneDirectory obj = new PhoneDirectory(maxNumbers); * int param_1 = obj.get(); * boolean param_2 = obj.check(number); * obj.release(number); */
```

4 segment Tree

O\(log n\) time in **allocate and release**

总共2\*max个节点，max个叶节点》max，max个内节点 《max。线段树是Bool arr

get取第一个超过max的未赋值，也就是叶节点。 每次使用叶节点或者释放，都要更新内节点。pushup

```text
class PhoneDirectory:    def __init__(self, maxNumbers: int):        """        Initialize your data structure here        @param maxNumbers - The maximum numbers that can be stored in the phone directory.        """        self.max = maxNumbers        self.segTree = [True]*(self.max << 1)        def pushup(self, i) -> None:        i >>=1        while i > 0:            self.segTree[i] =  self.segTree[i<<1] or self.segTree[i<<1|1]            i>>=1    def get(self) -> int:        """        Provide a number which is not assigned to anyone.        @return - Return an available number. Return -1 if none is available.        """        if not self.segTree[1]:            return -1        i = 1        while i < self.max:            if (i << 1) < (self.max << 1) and  self.segTree[i<<1]:                i = i<<1            if i<< 1|1 < self.max << 1 and  self.segTree[i<<1|1]:                i = i << 1|1        self.segTree[i] = False           res = i - self.max        self.pushup(i)        return res                                        def check(self, number: int) -> bool:        """        Check if a number is available or not.        """        if 0<=number < self.max:            return self.segTree[number + self.max]        return False            def release(self, number: int) -> None:        """                Recycle or release a number.        """        i = number+self.max        self.segTree[i] = True        self.pushup(i)                # Your PhoneDirectory object will be instantiated and called as such:# obj = PhoneDirectory(maxNumbers)# param_1 = obj.get()# param_2 = obj.check(number)# obj.release(number)
```

