# Perfect Squares

Given a positive integern, find the least number of perfect square numbers \(for example,`1, 4, 9, 16, ...`\) which sum ton.

**Example 1:**

```text
Input:
n
 = 
12
Output:
 3 

Explanation: 
12 = 4 + 4 + 4.
```

**Example 2:**

```text
Input:
n
 = 
13
Output:
 2

Explanation: 
13 = 4 + 9.
```

分析

java，i,j都从1开始，跳过0的情况。

```text
class Solution {
    public int numSquares(int n) {
        int[] v = new int[n+1];
        Arrays.fill(v, Integer.MAX_VALUE);
        v[0] = 0;
        for (int i = 1; i < n+1; i++){
            for (int j =1; j*j <= i; j++){
                v[i] = Math.min(v[i],v[i-j*j]+1);
            }
        }
        return v[n];

    }
}
```

