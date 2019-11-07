# Word Pattern

Given a `pattern` and a string `str`, find if `str` follows the same pattern.

Here **follow** means a full match, such that there is a bijection between a letter in `pattern` and a **non-empty** word in `str`.

**Example 1:**

```text
Input: pattern = "abba", str = "dog cat cat dog"Output: true
```

**Example 2:**

```text
Input:pattern = "abba", str = "dog cat cat fish"Output: false
```

**Example 3:**

```text
Input: pattern = "aaaa", str = "dog cat cat dog"Output: false
```

**Example 4:**

```text
Input: pattern = "abba", str = "dog dog dog dog"Output: false
```

**Notes:**  
You may assume `pattern` contains only lowercase letters, and `str`contains lowercase letters that may be separated by a single space.

分析

2个map，存的是当前Index，每次比较map值，也就是之前index。

注意get（key,defaultvalue）用法，defaultvalue要用-1 不能用0.

```text
class Solution:    def wordPattern(self, pattern: str, str: str) -> bool:        str = str.split(' ')        if len(str) != len(pattern):            return False        # wordsMap = {}        # for i in range(len(str)):        #     if pattern[i] in wordsMap and wordsMap[pattern[i]] != str[i]:        #          return False        #     if pattern[i] not in wordsMap:        #         if str[i] in wordsMap.values():        #             return False        #         wordsMap[pattern[i]] = str[i]        # return True        s,p = {},{}        for i in range(len(str)):            if s.get(str[i],-1) != p.get(pattern[i],-1): #default index必须是-1,因为0是有效Index                return False            s[str[i]] = p[pattern[i]] = i        return True                    
```

