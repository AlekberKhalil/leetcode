# Kth Smallest Number in Sorted Matrix

```text
Kth Smallest Number in Sorted Matrix
```

Find the\_k\_th smallest number in at row and column sorted matrix.

**Example**

Given k =`4`and a matrix:

```text
[
  [1 ,5 ,7],
  [3 ,7 ,8],
  [4 ,8 ,9],
]
```

return`5`

分析

和上面那题Kth largest element完全一样，复制的代码改了坐标，注意下是第几小所以k正序。坐标转换一下即可。 nums\[index/m\]\[index%m\]

最后是九章的heap算法，堆的大小无关，重要的是loop 0-k-1。matrix有序所以x+1,y+1加入的都是递增的数。每次加入新数就会挤掉最小元素，也就是头元素Pair cur = minHeap.poll\(\); loop k-1次后顶端元素就是最小kth。注意\(0,0\)并未入堆过。

```text
public class Solution {
    /*
     * @param matrix: a matrix of integers
     * @param k: An integer
     * @return: the kth smallest number in the matrix
     */
     int m, n;
    public int kthSmallest(int[][] matrix, int k) {
        // write your code here
        if(matrix == null || matrix.length == 0 || matrix[0] == null ||  matrix[0].length == 0)
            return -1;
        n = matrix.length;
        m = matrix[0].length;
        return helper(matrix, 0, n*m - 1, k);
    }

    private int helper(int[][] nums, int l, int r, int k){
       if (l == r) {
            return nums[l/m][l%m];
        }
        int index = partition(nums, l, r);
        if(index == k - 1){
                return nums[index/m][index%m];
            }else if(index > k-1){
                return helper(nums, l, index - 1, k);
            }else{
                return helper(nums, index + 1, r, k);
            }

    }

    private int partition(int[][] nums, int l, int r){
        int left = l, right = r, pivot = nums[left/m] [left%m];
        while(left < right){
            while(left < right && nums[right/m][right%m] >= pivot){
                right --;
            }
            nums[left/m] [left%m] = nums[right/m][right%m];
            while(left < right && nums[left/m] [left%m]<= pivot){
                left ++;
            }
            nums[right/m][right%m] = nums[left/m] [left%m];
        }
        nums[left/m] [left%m] = pivot;

        return left;

    }
}
```

heap

```text
public class Solution {
    /*
     * @param matrix: a matrix of integers
     * @param k: An integer
     * @return: the kth smallest number in the matrix
     */
    public int kthSmallest(int[][] matrix, int k) {
        // write your code here
        int n = matrix.length, m = matrix[0].length;
        PriorityQueue<Integer> q = new PriorityQueue<Integer>(k);
        for(int i = 0; i < matrix.length; i++){
            for(int j = 0; j < matrix[0].length; j++){
                    q.add(matrix[i][j]);
            }
        }
        int ret = 0;
        for(int i = 0; i < k; i++)
            ret = q.poll();
        return ret;
    }
}
```

```text
class Pair {
    public int x, y, val;
    public Pair(int x, int y, int val) {
        this.x = x;
        this.y = y;
        this.val = val;
    }
}
class PairComparator implements Comparator<Pair> {
    public int compare(Pair a, Pair b) {
        return a.val - b.val;
    }
}

public class Solution {
    /**
     * @param matrix: a matrix of integers
     * @param k: an integer
     * @return: the kth smallest number in the matrix
     */
    public int kthSmallest(int[][] matrix, int k) {
        // write your code here
        int[] dx = new int[]{0, 1};
        int[] dy = new int[]{1, 0};
        int n = matrix.length;
        int m = matrix[0].length;
        boolean[][] hash = new boolean[n][m];
        PriorityQueue<Pair> minHeap = new PriorityQueue<Pair>(k, new PairComparator());
        minHeap.add(new Pair(0, 0, matrix[0][0]));

        for(int i = 0; i < k - 1; i ++){
            Pair cur = minHeap.poll();
            for(int j = 0; j < 2; j ++){
                int next_x = cur.x + dx[j];
                int next_y = cur.y + dy[j];
                Pair next_Pair = new Pair(next_x, next_y, 0);
                if(next_x < n && next_y < m && !hash[next_x][next_y]){
                    hash[next_x][next_y] = true;
                    next_Pair.val = matrix[next_x][next_y];
                    minHeap.add(next_Pair);
                }
            }
        }
        return minHeap.peek().val;
    }
}
```

