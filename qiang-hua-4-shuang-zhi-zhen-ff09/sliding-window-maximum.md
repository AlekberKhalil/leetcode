# Sliding Window Maximum

Given an array of n integer with duplicate number, and a moving window\(size k\), move the window at each iteration from the start of the array, find the maximum number inside the window at each moving.

**Example**

For array`[1, 2, 7, 7, 8]`, moving window size`k = 3`. return`[7, 7, 8]`

At first the window is at the start of the array like this

`[|1, 2, 7| ,7, 8]`, return the maximum`7`;

then the window move one step forward.

`[1, |2, 7 ,7|, 8]`, return the maximum`7`;

then the window move one step forward again.

`[1, 2, |7, 7, 8|]`, return the maximum`8`;

分析

Deque双端队列, deque就是linkedlist ,deque 两头都可进可出 ,deque里元素单调递减

Deque offer，add加入末尾，push加入头

O\(N\*K\),每个元素都push 和pop一次 2n，所以是O\(N\)

用Deque双端队列来解。分为添加元素和删除元素两部步。

1. 初始化第一个窗口（0-第k－1个元素），一次向deque中加入数组中的元素。每次加入新元素时，若deque中最后一个元素比新元素小，则删去，直到deque中最后一个元素比新元素大时停止（或deque为空时停止），然后加入新元素。
2. 添加元素：从第k的元素开始，每次加入新元素时，若deque中最后一个元素比新元素小，则删去，直到deque中最后一个元素比新元素大时停止（或deque为空时停止），然后加入新元素。此时deque中第一个元素即为当前窗口的最大值，加入答案中。
3. 删除元素：应该删去（当前位置－k）位置的元素，看deque第一个元素是否和要删除元素相等，若不相等则说明在之前的元素加入过程中该元素已经删去，则不用做任何操作，否则删去deque中第一个元素即可。

```text
public class Solution {    /**     * @param nums: A list of integers.     * @return: The maximum number inside the window at each moving.     */    private void inQueue(Deque<Integer> q, int num){        while(!q.isEmpty() && q.peekLast() < num){            q.pollLast();        }        q.offer(num);    }    private void outQueue(Deque<Integer> q, int num){        if(num == q.peekFirst()){            q.pollFirst();        }    }    public ArrayList<Integer> maxSlidingWindow(int[] nums, int k) {        // write your code here        int n = nums.length;       Deque<Integer> q = new ArrayDeque<Integer>();       ArrayList<Integer> ret = new ArrayList<Integer>();       if(n == 0)           return ret;       //只到k-1因为k开始需要取结果了，之前不需要取只需要加数字        for(int i = 0; i < k-1; i ++){           inQueue(q, nums[i]);        }        for(int i = k-1; i < n; i ++){            inQueue(q, nums[i]);            ret.add(q.peekFirst());            outQueue(q, nums[i-k+1]);        }        return ret;    }}
```

python

入列：维持递减队列（每个数进入dp，把比他小的都弹出），最大的总在队首，每次队首加入res

出列：队首和nums\[i-k+1\]比较，==就弹出，不是的话证明dp size不够K，不必弹

```text
双端队列(Deque),可以维持一个递增的双端队列EX:[|1, 4|, 5, 3, 9], k = 3我们先将k-1个元素放入队列:|2|然后从第k个元素开始，一次加入新元素并删除旧元素，并且保持滑动窗口的size不变[|1, 4, 5|, 3, 9], Deque: 5, Output: [5];[1, |4, 5, 3|, 9], Deque: 5, 5, Output: [5, 5];[1, 4, |5, 3, 9|], Deque: 8, Output: [5, 5, 8];因为对于每个数组中的元素只扫描一次，所以总体时间在deque操作中也近似于线性，所以总运行时间：O(n)(amortized), 空间复杂度:O(1)
```

```text
class Solution:    def maxSlidingWindow(self, nums: List[int], k: int) -> List[int]:        if not nums:            return []        dq = collections.deque()        for i in range(k-1):            self.inQueue(dq, nums[i])#初始只到k-1,不到k，并且这里也要pop q if necessary        l = len(nums)        res = []        for i in range(k-1, l):            self.inQueue(dq, nums[i])            res.append(dq[0])            self.outQueue(dq, nums[i-k+1])        return res    def inQueue(self, dq:collections.deque, k: int):        while dq and dq[-1]  < k:            dq.pop()        dq.append(k)    def outQueue(self, dq:collections.deque, k: int):        if dq[0] == k:            dq.popleft()
```

