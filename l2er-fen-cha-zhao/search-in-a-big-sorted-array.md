# Search in a Big Sorted Array

题目：

Given a big sorted array with positive integers sorted by ascending order. The array is so big so that you can not get the length of the whole array directly, and you can only access the kth number by ArrayReader.get\(k\) \(or ArrayReader-&gt;get\(k\) for C++\). Find the first index of a target number. Your algorithm should be in O\(log k\), where k is the first index of the target number.

Return -1, if the number doesn't exist in the array.

分析：

这题目其实主要考察个如何“倍增”，二分法的内容其实没啥区别。

首先可以确定的是，倍增到-1为止或者倍增到大于target，接下来用二分法找first element。需要注意一点，如果get\(mid\) == -1的话说明mid已经超出范围了，需要让end = mid；

解法：

```text
class Solution {
public:
    /**
     * @param reader: An instance of ArrayReader.
     * @param target: An integer
     * @return: An integer which is the first index of target.
     */
    int searchBigSortedArray(ArrayReader *reader, int target) {
        // write your code here
        int index = 0;
        while (reader->get(index) != -1 && reader->get(index) < target ) {
            index = index * 2 + 1;
        }

        int start = 0;
        int end = index;

        while (start + 1 < end) {
            int mid = start + (end - start) / 2;
            if (reader->get(mid) == target) {
                end = mid;
            } else if (reader->get(mid) == -1 || reader->get(mid) > target) {
                end = mid;
            } else {
                start = mid;
            }
        }

        if (reader->get(start) == target) {
            return start;
        }

        if (reader->get(end) == target) {
            return end;
        }

        return -1;
    }
};
```

```text
public class Solution {
    /**
     * @param reader: An instance of ArrayReader.
     * @param target: An integer
     * @return : An integer which is the index of the target number
     */
    public int searchBigSortedArray(ArrayReader reader, int target) {
        // write your code here
        if (reader == null) {
            return -1;
        }
        int start = 0;
        int end = Integer.MAX_VALUE;
        int res = -1;
        while (start <= end) {
            int mid = start + (end - start) / 2;
            if (reader.get(mid) == -1) {
                end = mid - 1;
                continue;
            }
            if (reader.get(mid) == target) {
                res = mid;
                end = mid - 1;
            } else if (reader.get(mid) < target) {
                start = mid + 1;
            } else {
                end = mid - 1;
            }
        }
        return res;
    }
}
```

