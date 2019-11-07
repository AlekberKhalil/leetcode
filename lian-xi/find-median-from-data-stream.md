# Find Median from Data Stream

Median is the middle value in an ordered integer list. If the size of the list is even, there is no middle value. So the median is the mean of the two middle value.

`[2,3,4]`, the median is`3`

`[2,3]`, the median is`(2 + 3) / 2 = 2.5`

Design a data structure that supports the following two operations:

* void addNum\(int num\) - Add a integer number from the data stream to the data structure.
* double findMedian\(\) - Return the median of all elements so far.

For example:

```text
addNum(1)
addNum(2)
findMedian() -> 1.5
addNum(3) 
findMedian() -> 2
```

分析

用俩堆，每个各装一半，每次都是先入大堆，大堆再分给小堆。 除非大堆小了，再调整回去。

只是小堆都是负数。然后始终保持大堆大一个

```text
class MedianFinder {
//大小堆，2个都装，小的装负数，始终保持大堆大一点。
    /** initialize your data structure here. */
    Queue<Long> max;
    Queue<Long> min;
    public MedianFinder() {
        max = new PriorityQueue<>();
        min = new PriorityQueue<>();
    }

    public void addNum(int num) {
        max.offer((long)num);
        min.offer(-max.poll());
        if(max.size() < min.size()){
            max.offer(-min.poll());
        }
    }

    public double findMedian() {
        if(max.size() > min.size()){
            return max.peek();
        }else{
            return (max.peek() - min.peek()) / 2.0; //2.0啊这里！！！！！
        }
    }
}

/**
 * Your MedianFinder object will be instantiated and called as such:
 * MedianFinder obj = new MedianFinder();
 * obj.addNum(num);
 * double param_2 = obj.findMedian();
 */
```

