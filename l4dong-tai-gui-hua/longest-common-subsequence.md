# Longest Common Subsequence

Given two strings, find the longest common subsequence \(_LCS_\).

Your code should return the length of_LCS_.

**Example**

For`"ABCD"`and`"EDCA"`, the\_LCS\_is`"A"`\(or`"D"`,`"C"`\), return`1`.

For`"ABCD"`and`"EACB"`, the\_LCS\_is`"AC"`, return`2`.

分析

2个seq的话，distance\[i\]\[j\]代表word1的前i个字符匹配上word2的前j个字符， 枚举2个字符串的所有位置

```text
public class Solution {
    /**
     * @param A, B: Two strings.
     * @return: The length of longest common subsequence of A and B.
     */
    public int longestCommonSubsequence(String A, String B) {

        int[][] f = new int[A.length() + 1][B.length() + 1];
        for(int i = 1; i <= A.length(); i ++){
            for(int j = 1; j <= B.length(); j ++){
                if(A.charAt(i-1) == B.charAt(j-1)){
                    f[i][j] = f[i-1][j-1] + 1;
                }
                f[i][j] = Math.max(f[i][j], Math.max(f[i-1][j],f[i][j-1]));
            }
        }
        return f[A.length()][B.length()];

        // write your code here
        // int m = A.length();
        // int n=B.length();

        // char[] ac = A.toCharArray();
        // char[] bc = B.toCharArray();

        // int[][] f= new int[m+1][n+1];

        // for(int i=1;i<=m;i++){
        //     for(int j=1;j<=n;j++){
        //         if(ac[i-1]==bc[j-1])
        //             f[i][j]=f[i-1][j-1]+1;

        //         f[i][j]=Math.max(f[i][j],Math.max(f[i-1][j],f[i][j-1]));
        //     }
        // }

        // return f[m][n];
    }
}
```

