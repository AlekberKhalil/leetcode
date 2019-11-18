# Minimum Window Substring（FB 模板）

Given a string source and a string target, find the minimum window in source which will contain all the characters in target.

## Notice

If there is no such window in source that covers all characters in target, return the emtpy string`""`.

If there are multiple such windows, you are guaranteed that there will always be only one unique minimum window in source.

**Clarification**

Should the characters in minimum window has the same order in target?

* Not necessary.

**Example**

For source =`"ADOBECODEBANC"`, target =`"ABC"`, the minimum window is`"BANC"`

分析

前向型追击指针,target和source都分别放入俩hash, 或者int\[256\],比较俩大小

要考虑有数字或者字符，所以用256而非26

还是按模板写吧。

第二种做法

[http://blog.hyoung.me/cn/2017/02/minimum-window-substring/](http://blog.hyoung.me/cn/2017/02/minimum-window-substring/)

还是双指针，只是判断source和target是否相等时，用sourceCount,。先用target初始化HashMap&lt;Character, Integer&gt; map

若遇到char在target中的，则sourceCount ++。同时target的hashmap里count--。

答案

```text
     private boolean valid(int[] source, int[] target){
        for(int i = 0; i < 256; i ++){
            if(source[i] < target[i])
                return false;
        }
        return true;
     }
    public String minWindow(String source, String target) {
        // write your code
        int[] s = new int[256];
        int[] t = new int[256];

        int ret = Integer.MAX_VALUE;
        char[] cs = target.toCharArray();
        for(char c : cs){
            t[c] ++;
        }
        String sret = "";
        int n = source.length(), m = target.length();
        for(int i = 0, j = 0; i < n; i ++){
            while(j < n){
                if(!valid(s,t) && j < n){
                     s[source.charAt(j) ] ++;
                     j ++;
                }else{
                    break;
                }

            }

            if(valid(s,t) && j-i < ret){
                       sret = source.substring(i, j); 
                       ret = j - i;
                    }

            s[source.charAt(i)] --;
        }

        return sret;
    }
```

```text
    public String minWindow(String source, String target) {
       HashMap<Character, Integer> map = new HashMap<Character, Integer>();
        char[] cs = target.toCharArray();
        for(char c : cs){
            if(map.containsKey(c)){
                map.put(c, map.get(c) + 1);
            }else{
                map.put(c, 1);
            }
        }
        int ret = Integer.MAX_VALUE;
        String sret = "";
        int n = source.length(), m = target.length(), sourceCnt = 0;

        for(int i = 0, j = 0; i < n; i ++){
            while(j < n && sourceCnt < m){
                char cur = source.charAt(j);
                if(map.containsKey(cur)){
                     if(map.get(cur) > 0){
                         sourceCnt ++;
                     }
                     map.put(cur, map.get(cur) - 1);
                }
                j ++;
            }

            if(sourceCnt == m && j-i < ret){
               sret = source.substring(i, j); 
               ret = j - i;
            }

            char start = source.charAt(i);
            if(map.containsKey(start)){
                 if(map.get(start) >= 0){
                     sourceCnt --;
                 }
                 map.put(start, map.get(start) + 1);
            }
        }

        return sret;
    }
```

python

2个dict存s,t的count，isvalid函数判断是否t在s内：sl\[i\] &lt; tl\[i\]

前向追击指针，sdict,ldict count ++/--控制

```text
import collections


class Solution:
    def minWindow(self, s, t):
        """
        :type s: str
        :type t: str
        :rtype: str
        """
        n = len(s)

        if not s or not t or len(s) < len(t):
            return ""
        j = 0
        minlen = len(s) + 1
        ret = ""
        sl = collections.defaultdict(int)
        tl = collections.defaultdict(int)

        for i in t:
            tl[i] += 1

        for i in range(n):
            while j < n:
                if not self.isValid(sl, tl) and j< n:
                    sl[s[j]] += 1
                    j += 1
                else:
                    break
            if self.isValid(sl, tl) and j - i < minlen:
                    minlen = j - i
                    ret = s[i:j]
            sl[s[i]] -= 1

        return ret

    def isValid(self, sl, tl):
        for i in tl:
            if i not in sl or sl[i] < tl[i]:
                return False
        return True
```

根据模板写的

**一个map存char count。头尾指针，尾前进到满足条件，头缩进到不满足条件。2个while一个头一个尾。注意min/max的位置**

```text
这里注意

if map[s[end]]>0:#只要有存在（>=1）都要减
counter -= 1

if map[s[start]] == 0: #只有map==0才是正好满足全部包含的临界情况，负数代表多了
counter += 1
```

```text
import collections


class Solution:
    def minWindow(self, s, t):
        """
        :type s: str
        :type t: str
        :rtype: str
        """
        start=end = 0
        d=len(s)+1
        ret=""
        counter = len(t)
        map = collections.defaultdict(int)
        n = len(s)
        for i in t:
            map[i]+=1
        while end < n:
            if map[s[end]]>0:
                counter -= 1
            map[s[end]]-=1
            end+=1
            while counter == 0:
                if end-start<d:
                    d = end-start
                    ret = s[start:end]
                if map[s[start]] == 0:
                    counter += 1
                map[s[start]]+=1
                start += 1
        return ret
```

jiuzhang的模板做 for start，while end

```text
import collections


class Solution:
    def minWindow(self, s, t):
        """
        :type s: str
        :type t: str
        :rtype: str
        """
        start=end = 0
        d=len(s)+1
        ret=""
        counter = len(t)
        map = collections.defaultdict(int)
        for i in t:
            map[i] += 1
        n = len(s)
        for start in range(n):
            while end < n and counter > 0:
                if map[s[end]] > 0:
                    counter -= 1
                map[s[end]]-=1
                end+=1
            if counter == 0:
                if d > end-start:
                    d = end-start
                    ret = s[start:end]
                if map[s[start]]==0:
                    counter += 1
                map[s[start]] += 1
        return ret
```

