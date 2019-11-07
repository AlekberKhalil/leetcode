# strStr

```text
For a given source string and a target string, you should output thefirstindex(from 0) of target string in source string.
```

If target does not exist in source, just return`-1`.

Do I need to implement KMP Algorithm in a real interview?

* Not necessary. When you meet this problem in a real interview, the interviewer may just want to test your basic implementation ability. But make sure your confirm with the interviewer first.

**Example**

If source =`"source"`and target =`"target"`, return`-1`.

If source =`"abcdabcdefg"`and target =`"bcd"`, return`1`.

分析

起点从i开始Loop，注意边界i到source.length\(\) - target.length\(\) + 1。j是长度。当j达到target长度就找到了起点i。

答案

```text
public int strStr(String source, String target) {        // write your code here        if(source == null || target == null)            return -1;        int sl = source.length();        int tl = target.length();            if(tl == 0)                return 0;        for(int i = 0; i < sl - tl + 1; i ++){            int j = 0;            for(j = 0; j < tl; j ++){                if(source.charAt(i + j) != target.charAt(j)){                    break;                }             if(j == tl - 1){                        return i;                    }               }        }        return -1;    }
```

python做法

需要保持一个fixed sliding window的长度为短字符串的长度然后扫长字符串来寻找起始位置

难点还是index

```text
class Solution:    def strStr(self, haystack: str, needle: str) -> int:        e,l,p = 0,len(haystack),len(needle)        while e < l - p + 1: #依然是Index，只能i - len + 1            if haystack[e:e+p] == needle: #这里可以直接 j+len                 return e            e += 1        return -1
```

