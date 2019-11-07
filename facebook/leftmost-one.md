# Leftmost One

Given a 2D array, and each line has only`0`and`1`, the front part is`0`, and the latter part is`1`. Find the number of columns in the leftmost`1`of all the rows in the array.

## Example

Given arr =`[[0,0,0,1],[1,1,1,1]]`, return`0`.

```text
Explanation:Arr[1][0] is the leftmost 1 in all rows and its column is 0.
```

Given arr =`[[0,0,0,1],[0,1,1,1]]`, return`1`.

```text
Explanation:Arr[1][1] is the leftmost 1 in all rows and its column is 1.
```

## Notice

* The number of rows in the array and the number of columns do not exceed

  `1000`

* In order to limit the time complexity, your program will run

  `50000`

  times

分析

充分利用前面部分是0，后一部分是1二维数组的性质。找到第0行第一个1，然后往下找，是0就continue，是1的话往前找。时间复杂度O\(m+n\)。

```text
class Solution:    """    @param arr: The 2-dimension array    @return: Return the column the leftmost one is located    """    def getColumn(self, arr):        # Write your code here        if not arr or not arr[0]:            return -1        n = len(arr)        m = len(arr[0])        idx = m-1        for row in arr:            while idx >=0:                if row[idx] == 0:                    break                idx -=1        return idx+1
```

