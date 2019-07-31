# Word Break

Given a**non-empty**stringsand a dictionarywordDictcontaining a list of**non-empty**words, determine ifscan be segmented into a space-separated sequence of one or more dictionary words. You may assume the dictionary does not contain duplicate words.

For example, given  
s=`"leetcode"`,  
dict=`["leet", "code"]`.

Return true because`"leetcode"`can be segmented as`"leet code"`.

分析

和前面一题的划分一样，也是sequence。i长度n+1,j等于i-1。条件判断时不取到i

这里得到f\[i\]为true时就break!!!!!!!!!!!

```text
class Solution {
    public boolean wordBreak(String s, List<String> wordDict) {
        int n = s.length();
        boolean[] f = new boolean[n + 1];
        f[0] = true;
        for(int i = 1; i <= n; i ++){
            for(int j = 0; j < i; j ++){
                    if(f[j] && wordDict.contains(s.substring(j, i))){
                        f[i] = true;#能true就出来 不要一直做
                        break;
                    }
                }
            }
        return f[n];
        }            
}
```

