# Brick Wall

```text
You cannot draw a line just along one of the two vertical edges of the wall, in which case the line will obviously cross no bricks.

Example:
Input: 
[[1,2,2,1],
 [3,1,2],
 [1,3,2],
 [2,4],
 [3,1,2],
 [1,3,1,1]]
Output: 2
Explanation:


Note:
The width sum of bricks in different rows are the same and won't exceed INT_MAX.
The number of bricks in each row is in range [1,10,000]. The height of wall is in range [1,10,000]. Total number of bricks of the wall won't exceed 20,000.
```

分析

求每个row的presum,看看哪个sum的个数最多就作为分割线。结果width- \# of max \(count of presum\)

注意此处统计presum个数不用list用map,因为10，000超过Int,用map的话Key是string

```text
class Solution:
    def leastBricks(self, wall):
        """
        :type wall: List[List[int]]
        :rtype: int
        """
        if not wall or len(wall) == 0:
            return 0
        rowLen = len(wall)
        sumCnt = collections.defaultdict(int)
        for row in wall:
            prevSum = 0
            for j in row[:-1]:
                prevSum += j
                sumCnt[prevSum] += 1

        return rowLen - max(sumCnt.values() if len(sumCnt) > 0 else [0])
```

