# Sliding Window Matrix Maximum

## Sliding Window Matrix Maximum <a id="sliding-window-matrix-maximum-558"></a>

### Question <a id="question"></a>

Given an array of n\_m matrix, and a moving matrix window \(size k\_k\), move the window from top left to botton right at each iteration, find the maximum sum of the elements inside the window at each moving. Return 0 if the answer does not exist.

Example

For matrix

\[ \[1, 5, 3\], \[3, 2, 1\], \[4, 1, 9\], \]

The moving window size k = 2.

return 13.

At first the window is at the start of the array like this

\[ \[\|1, 5\|, 3\], \[\|3, 2\|, 1\], \[4, 1, 9\], \]

,get the sum 11;

then the window move one step forward.

\[ \[1, \|5, 3\|\], \[3, \|2, 1\|\], \[4, 1, 9\], \]

,get the sum 11;

then the window move one step forward again.

\[ \[1, 5, 3\], \[\|3, 2\|, 1\], \[\|4, 1\|, 9\], \]

,get the sum 10;

then the window move one step forward again.

\[ \[1, 5, 3\], \[3, \|2, 1\|\], \[4, \|1, 9\|\], \] ,get the sum 13;

SO finally, get the maximum from all the sum which is 13.

Challenge

O\(n^2\) time.

### Solution <a id="solution"></a>

Presum的题目，以某数字结尾左上所有元素sum，左和上一定要加dummy 0行/列 好算（左边和上面围两条0）

sum\[i\]\[j\]表示0-i－1行和0-j－1列所有元素的和。

1. 建立sum矩阵，为n＋1行，m＋1列。将第0行和第0列都初始化为0。
2. 遍历matrix，以某数字结尾左上所有元素sum，根据公式 sum\[i\]\[j\] = matrix\[i - 1\]\[j - 1\] + sum\[i\]\[j - 1\] + sum\[i - 1\]\[j\] -sum\[i - 1\]\[j - 1\] 计算所有sum。
3. 然后计算每个窗口的sum，根据公式 sum = sum\[i\]\[j\] - sum\[i - k\]\[j\] - sum\[i\]\[j - k\] + sum\[i - k\]\[j - k\] 即整个大窗口剪去上面一部分和左边一部分再加回被重复减去的部分，即为当前窗口值

## Answer

```text
public int maxSlidingWindow2(int[][] matrix, int k) {        if(matrix == null || matrix.length == 0 || matrix[0].length == 0 || k > matrix.length || k > matrix[0].length){            return 0;        }        int n = matrix.length, m = matrix[0].length;        int[][] sum = new int[n + 1][m + 1];        for(int i = 1; i <= n; i ++){            for(int j = 1; j <= m; j ++){                sum[i][j] = sum[i - 1][j] + sum[i][j - 1] - sum[i -1][j - 1] + matrix[i - 1][j - 1];            }        }        int max = Integer.MIN_VALUE;        for(int i = k + 1; i <= n; i ++) {            for (int j = k + 1; j <= m; j++) {                max = Math.max(max, sum[i][j] - sum [i - k][j] - sum[i][j - k] + sum[i - k][j - k]);            }        }        return max;    }
```

