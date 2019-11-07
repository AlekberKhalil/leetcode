# Longest Substring Without Repeating Characters

Given a string, find the length of the longest substring without repeating characters.

**Example**

For example, the longest substring without repeating letters for`"abcabcbb"`is`"abc"`, which the length is`3`.

For`"bbbbb"`the longest substring is`"b"`, with the length of`1`.

分析

前向型指针，子串子数组看成一个窗口满足某个条件，用hash，char做Index 256。while出来后要更新i状态。

1. visit 数组 cs\[char\] 而不是 char-'a'， 且数组长度是256，是为了防止特殊字符的出现
2. 长度是j-i 不是J-i+ 1
3. 开始不需要cs\[s.charAt\[i\]\] ++ 直接设置J就好
4. 模板很重要

答案

```text
public int lengthOfLongestSubstring(String s) {
        // write your code here
        int[] cs = new int[256];
        int n = s.length();
        int ret = 0;
        for(int i = 0, j = 0; i < n; i ++){
            while(j < n & cs[s.charAt(j)] == 0){
                cs[s.charAt(j)]++;
                j ++;
            }
            ret = Math.max(ret, j - i);
            cs[s.charAt(i)] = 0;
        }
        return ret;
    }
```

```text
#注意进出counter while的几个条件

import collections


class Solution:
    """
    @param s: a string
    @return: an integer
    """
    def lengthOfLongestSubstring(self, s):
        # write your code here
        counter=start=end=d=0
        map = collections.defaultdict(int)
        n = len(s)
        while end<n:
            if map[s[end]] > 0:
                counter+=1
            map[s[end]]+=1
            end+=1
            while counter>0:
                if map[s[start]]>1:
                    counter -=1
                map[s[start]] -=1
                start+=1
            d=max(d,end-start)
        return d
```

不用Map计算counter，用set也行

```text
class Solution:
    """
    @param s: a string
    @return: an integer
    """
    def lengthOfLongestSubstring(self, s):
        unique_chars = set([])
        j = 0
        n = len(s)
        longest = 0
        for i in range(n):
            while j < n and s[j] not in unique_chars:
                unique_chars.add(s[j])
                j += 1
            longest = max(longest, j - i)
            unique_chars.remove(s[i])

        return longest
```

loop start,比较上面的loop end

```text
import collections


class Solution:
    def lengthOfLongestSubstring(self, s):
        """
        :type s: str
        :rtype: int
        """
        if not s:
            return 0
        n = len(s)
        map = collections.defaultdict(int)
        end = d =0
        for start in range(n):
            while end < n and map[s[end]]==0:
                map[s[end]] += 1
                end+=1
            d = max(d,end-start)
            map[s[start]] -= 1
        return d
```

