# Find Peak Element II

There is an integer matrix which has the following features:

The numbers in adjacent positions are different.

The matrix has n rows and m columns.

For all i &lt; m, A\[0\]\[i\] &lt; A\[1\]\[i\] && A\[n - 2\]\[i\] &gt; A\[n - 1\]\[i\].

For all j &lt; n, A\[j\]\[0\] &lt; A\[j\]\[1\] && A\[j\]\[m - 2\] &gt; A\[j\]\[m - 1\].

We define a position P is a peek if:

A\[j\]\[i\] &gt; A\[j+1\]\[i\] && A\[j\]\[i\] &gt; A\[j-1\]\[i\] && A\[j\]\[i\] &gt; A\[j\]\[i+1\] && A\[j\]\[i\] &gt; A\[j\]\[i-1\]

Find a peak element in this matrix. Return the index of the peak.

Example

Given a matrix:

\[ \[1 ,2 ,3 ,6 ,5\], \[16,41,23,22,6\], \[15,17,24,21,7\], \[14,18,19,20,10\], \[13,14,11,10,9\] \]

return index of 41 \(which is \[1,1\]\) or index of 24 \(which is \[2,2\]\)

Challenge

Solve it in O\(n+m\) time.

If you come up with an algorithm that you thought it is O\(n log m\) or O\(m log n\), can you prove it is actually O\(n+m\) or propose a similar but O\(n+m\) algorithm?

分析

和在数组中find peak element一样，对行和列分别进行二分查找。

1. 先对行进行二分搜索，对搜到的那一行元素再进行二分搜索寻找peak element
2. 对找到的element看上下行的同列元素，若相同则返回，若比上小则在上半部分行继续进行搜索，若比下小则在下半部分的行继续进行搜索 o\(logn \*n\)
3. 也可以按列分，行列其实一样，行列交替的话O\(n\)，找每行/列最大数时候，记得for loop的start and end变换，不能直接拿整行和整列做。
4. 数组初始化arraylist

```text
        List<Integer> ret = Arrays.asList(x, y);        new ArrayList<>( Arrays.asList(1,2,3) )
```

答案

```text
public List<Integer> findPeak(int[][] matrix) {        if(matrix == null || matrix.length == 0 || matrix[0] == null || matrix[0].length == 0)            return null;        int n = matrix.length, m = matrix[0].length;        int sr = 1, er = n - 2, sc = 1, ec = m - 2, mid, temp;        while(sr + 1 < er && sc + 1 < ec){            mid = sr + (er - sr)/2;            temp = getMax(matrix, mid, sr, er,true);            if(matrix[mid][temp] < matrix[mid - 1][temp]){                er = mid;            }else if(matrix[mid][temp] < matrix[mid + 1][temp]){                sr = mid;            }else{                er = mid;            }            mid = sc + (ec - sc)/2;            temp = getMax(matrix, mid, sc, ec, false);            if(matrix[temp][mid] < matrix[temp][mid - 1]){                ec = mid;            }else if(matrix[temp][mid] < matrix[temp][mid - 1]){                sc = mid;            }else{                ec = mid;            }        }        int a  = matrix[sr][sc], x = sr, y = sc;        if(a < matrix[sr][ec]){            a = matrix[sr][ec];            x = sr;            y = ec;        }        if(a < matrix[er][sc]){            a = matrix[er][sc];            x = er;            y = sc;        }        if(a < matrix[er][ec]){            a = matrix[er][ec];            x = er;            y = ec;        }        List<Integer> ret = Arrays.asList(x, y);        //new ArrayList<>( Arrays.asList(1,2,3) )        return ret;    }    private int getMax(int[][] matrix, int mid, int s, int e, boolean isRow) {        int max = Integer.MIN_VALUE, ret = 0;        if (isRow) {            for (int i = s; i <= e; i++) {                if (matrix[mid][i] > max) {                    ret = i;                }            }            return ret;        } else {            for (int i = s; i <= e; i++) {                if (matrix[i][mid] > max) {                    ret = i;                }            }            return ret;        }    }
```

其实如果中间大于两边已经是峰值了，可以直接返回。

```text
public List<Integer> findPeak(int[][] matrix) {        List<Integer> ret = new ArrayList<Integer>();        if(matrix == null || matrix.length == 0 || matrix[0] == null || matrix[0].length == 0)            return ret;        int n = matrix.length, m = matrix[0].length;        int sr = 1, er = n - 2, sc = 1, ec = m - 2, mid, temp;        while(sr + 1 < er && sc + 1 < ec){            mid = sr + (er - sr)/2;            temp = getMax(matrix, mid, sr, er,true);            if(matrix[mid][temp] < matrix[mid - 1][temp]){                er = mid;            }else if(matrix[mid][temp] < matrix[mid + 1][temp]){                sr = mid;            }else{                sr = mid;                er = mid;                ret = Arrays.asList(sr, er);                break;            }            mid = sc + (ec - sc)/2;            temp = getMax(matrix, mid, sc, ec, false);            if(matrix[temp][mid] < matrix[temp][mid - 1]){                ec = mid;            }else if(matrix[temp][mid] < matrix[temp][mid - 1]){                sc = mid;            }else{                sc = mid;                ec = mid;                ret = Arrays.asList(sc, ec);                break;            }        }//        List<Integer> ret = Arrays.asList(x, y);        //new ArrayList<>( Arrays.asList(1,2,3) )        return ret;    }    private int getMax(int[][] matrix, int mid, int s, int e, boolean isRow) {        int max = Integer.MIN_VALUE, ret = 0;        if (isRow) {            for (int i = s; i <= e; i++) {                if (matrix[mid][i] > max) {                    ret = i;                }            }            return ret;        } else {            for (int i = s; i <= e; i++) {                if (matrix[i][mid] > max) {                    ret = i;                }            }            return ret;        }    }
```

