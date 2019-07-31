# Course Schedule III\(heap,sort\)

There are`n`different online courses numbered from`1`to`n`. Each course has some duration\(course length\)`t`and closed on`dth`day. A course should be taken**continuously**for`t`days and must be finished before or on the`dth`day. You will start at the`1st`day.

Given`n`online courses represented by pairs`(t,d)`, your task is to find the maximal number of courses that can be taken.

**Example:**

```text
Input:
 [[100, 200], [200, 1300], [1000, 1250], [2000, 3200]]

Output:
 3

Explanation:

There're totally 4 courses, but you can take 3 courses at most:
First, take the 1st course, it costs 100 days so you will finish it on the 100th day, and ready to take the next course on the 101st day.
Second, take the 3rd course, it costs 1000 days so you will finish it on the 1100th day, and ready to take the next course on the 1101st day. 
Third, take the 2nd course, it costs 200 days so you will finish it on the 1300th day. 
The 4th course cannot be taken now, since you will finish it on the 3300th day, which exceeds the closed date.
```

**Note:**  
The integer 1

1. The integer 1&lt;= d, t, n &lt;= 10,000.
2. You can't take two courses simultaneously.

分析

看到数组先排序，按照日期（c\[1\]）从小到大。 用priority queue存耗费天数 c\[0\]，按照从大小大。然后loop每个课程，都加入pq算天数。遇到不行的就从pq里弹出最大c\[0\]。

```text
class Solution {
    public int scheduleCourse(int[][] courses) {
        Comparator<int[]> comp = (c1, c2) ->  c1[1] - c2[1];
        Arrays.sort(courses, comp);
        PriorityQueue<int[]> pq = new PriorityQueue<>((a,b) -> b[0] - a[0]);

        int ds = 0;

        for(int[] c : courses) {                   
                 pq.offer(c);
                ds += c[0];                      
            if(ds  > c[1]){               
                ds -= pq.poll()[0];               
            }

        }
        return pq.size();

    }
}
```

