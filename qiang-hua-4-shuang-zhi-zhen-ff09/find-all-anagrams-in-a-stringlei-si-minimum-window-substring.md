# Find All Anagrams in a String\(类似Minimum Window Substring）

Given a string**s**and a**non-empty**string**p**, find all the start indices of**p**'s anagrams in**s**.

Strings consists of lowercase English letters only and the length of both strings**s**and**p**will not be larger than 20,100.

The order of output does not matter.

**Example 1:**

```text
Input:

s: "cbaebabacd" p: "abc"


Output:

[0, 6]


Explanation:

The substring with start index = 0 is "cba", which is an anagram of "abc".
The substring with start index = 6 is "bac", which is an anagram of "abc".
```

**Example 2:**

```text
Input:

s: "abab" p: "ab"


Output:

[0, 1, 2]


Explanation:

The substring with start index = 0 is "ab", which is an anagram of "ab".
The substring with start index = 1 is "ba", which is an anagram of "ab".
The substring with start index = 2 is "ab", which is an anagram of "ab".
```

分析

对比**Strstr。** 

相同点：

s,t length要一样。

不同点：

strStr 顺序需要，所以i,j初始就是t的间隔，每次比完一起走

anagram 顺序不需要，所以Map

类似Minimum Window Substring， 一个动态的滑动窗口指针，区别在if e - ss == len\(p\):得结果

**count遇到数字拐点0-》1 1-》0才会变化**，初始值为len\(t\)？？？

**if map: count 才++/--**

map和s,e总是要++/--

```text
class Solution:
    def findAnagrams(self, s: str, p: str) -> List[int]:
        mm = collections.defaultdict(int)
        count = 0
        for i in p:
            mm[i] +=1

        l = len(s)

        ss,e,counter =0,0,len(p)
        res = []
        while e < l : 
            if mm[s[e]] > 0:
                counter -= 1
            mm[s[e]] -= 1
            e += 1
            while counter == 0:
                if e - ss == len(p): #e已经到了下一位 所以可以直接用长度
                    res.append(ss)

                if mm[s[ss]] == 0:
                    counter += 1
                mm[s[ss]] += 1
                ss += 1
        return res
```

