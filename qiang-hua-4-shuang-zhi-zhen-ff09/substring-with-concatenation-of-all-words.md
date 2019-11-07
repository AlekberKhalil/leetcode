# Substring with Concatenation of All Words



You are given a string, **s**, and a list of words, **words**, that are all of the same length. Find all starting indices of substring\(s\) in **s** that is a concatenation of each word in **words** exactly once and without any intervening characters.

**Example 1:**

```text
Input:
  s = "barfoothefoobarman",
  words = ["foo","bar"]
Output: [0,9]
Explanation: Substrings starting at index 0 and 9 are "barfoor" and "foobar" respectively.
The output order does not matter, returning [9,0] is fine too.
```

**Example 2:**

```text
Input:
  s = "wordgoodgoodgoodbestword",
  words = ["word","good","best","word"]
Output: []
```

分析

就是needle in haystack, target数组所有字符都在而且连续，顺序可以不计，所以用Map

维护i在s里，经过所有s位置，到target总长度位置，记得这里要+1

内循环维护j，每个词每个词的跳，最后判断j == target words total

这里内循环用新map判断合法。

```text
class Solution {
    public List<Integer> findSubstring(String s, String[] words) {
        List<Integer> res = new ArrayList<>();
        int nw = words.length,ns = s.length();
        
        if(nw == 0){
            return res;
        }
        int wlen = words[0].length();
        Map<String,Integer> mm = new HashMap<>();
        for(String w : words){
            mm.put(w, mm.getOrDefault(w,0) + 1);
        }
        for(int i = 0; i < ns - nw*wlen+1; i++){//这里end要+1
            Map<String,Integer> seen = new HashMap<>();
            int j = 0;
            while(j < nw){
                String cur = s.substring(i + j*wlen, i + (j+1) *wlen);  //end没有+1这里             
                if(mm.containsKey(cur)){
                    seen.put(cur,seen.getOrDefault(cur,0) + 1);
                    if(seen.get(cur) > mm.get(cur)){
                        break;
                    }
                }else{
                    break;
                }
                j ++;
            }
            if(j == nw){
                res.add(i);
            }
        }
        return res;
    }
}
```

Python

```text
class Solution:
    def findSubstring(self, s: str, words: List[str]) -> List[int]:
        res = []
        if not words:
            return res
        mm = {}
        for w in words:
            mm[w] = mm.get(w,0)+1
        i,wlen,nw = 0,len(words[0]),len(words)
        for i in range(len(s) - nw*wlen+1) :
            j,seen = 0,{}
            while j < nw:
                cur = s[i+j*wlen:i+(j+1)*wlen]
                if cur not in mm:
                    break
                seen[cur] = seen.get(cur,0) +1
                if seen[cur] > mm[cur]:
                    break;
                j += 1
                if j == nw:
                    res.append(i)
        return res
                
            
            
        
```

