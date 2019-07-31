# Interleaving String

Givens1,s2,s3, find whethers3is formed by the interleaving ofs1ands2.

For example,  
Given:  
s1=`"aabcc"`,  
s2=`"dbbca"`,

Whens3=`"aadbbcbcac"`, return true.  
Whens3=`"aadbbbaccc"`, return false.

分析

s1, s2的最后字母和s3比较

```text
table[i][j] = (table[i-1][j] && s1[i-1] == s3[i+j-1] ) || (table[i][j-1] && s2[j-1] == s3[i+j-1] );
```

初始化里也要考虑前面的f

f\[0\]\[j\] = **f\[0\]\[j - 1\]** && s3.charAt\(j- 1\) == s2.charAt\(j - 1\);

```text
class Solution {
    public boolean isInterleave(String s1, String s2, String s3) {
        int n = s1.length();
        int m = s2.length();
        int k = s3.length();
        if(n + m != k) 
            return false;
        boolean[][] f = new boolean[n + 1][m + 1];
        //不能在循环里初始化，是为了防止a,b的长度不足1时候。
            for(int i = 0; i <= n; i ++){                
                for(int j = 0; j <= m; j ++){
                    if(i == 0 && j == 0){
                        f[i][j] = true;
                    }else if(i == 0){
                        f[i][j] = f[i][j - 1] && s3.charAt(j- 1) == s2.charAt(j - 1);
                    }else if(j == 0){
                        f[i][j] = f[i - 1][j] && s3.charAt(i - 1) == s1.charAt(i - 1);
                    }else{
                        f[i][j] = s3.charAt(i + j - 1) == s1.charAt(i-1) && f[i - 1][j] //用i所以f里i-1
                        || s3.charAt(i + j - 1) == s2.charAt(j-1) && f[i][j - 1];
                    }            
                    }                                       
                }



        return f[n][m];
    }
}
```

