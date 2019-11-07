# Word Ladder

Given two words \(beginWordandendWord\), and a dictionary's word list, find the length of shortest transformation sequence frombeginWordtoendWord, such that:

1. Only one letter can be changed at a time.
2. Each transformed word must exist in the word list. Note that beginWord is not a transformed word.

For example,

Given:  
beginWord=`"hit"`  
endWord=`"cog"`  
wordList=`["hot","dot","dog","lot","log","cog"]`

As one shortest transformation is`"hit" -> "hot" -> "dot" -> "dog" -> "cog"`,  
return its length`5`.

**Note:**

* Return 0 if there is no such transformation sequence.
* All words have the same length.
* All words contain only lowercase alphabetic characters.
* You may assume no duplicates in the word list.
* You may assume beginWord and endWord are non-empty and are not the same.

分析

BFS，while里for size,然后level ++ ，直接返回，因为第一个到的就是最短的。

这里字典转化成hashset，因为hashset的contains复杂度是o\(1\)，而arraylist或者Linkedlist都是O（N\)

```text
class Solution {
    public int ladderLength(String beginWord, String endWord, List<String> wordList) {

        return bfs(beginWord, endWord, wordList);
    }

    List<String> getNextWord(String cur, Set
                             <String> wordList){
        List<String> ret = new ArrayList<String>();
        char[] cs = cur.toCharArray();
        for(int i = 0; i < cur.length(); i ++){                   
            for(char c = 'a' ; c <= 'z'; c ++){
                if(cs[i] == c){
                    continue;
                }                    
                char temp = cs[i];
                cs[i] = c;
                String nw = new String(cs);                
                if(wordList.contains(nw)){
                    ret.add(nw);
                }
                cs[i] = temp;
            }                
        } 
        return ret;
    }

    int bfs(String beginWord, String endWord, List<String> wordList){
        Queue<String> q = new LinkedList<String>();
        Set<String> set = new HashSet<String>();
        //用set存字典，为了让查contains更快
        Set<String> dict = new HashSet<>();
        for (String word : wordList) {
            dict.add(word);
        }
        q.add(beginWord);
        //wordList.add(beginWord);
        int level = 1;

        while(!q.isEmpty()){ 
            level ++;
            int size = q.size();
            for(int i = 0; i < size; i ++){
                String cur = q.poll();
                List<String> nextWords = getNextWord(cur, dict);
                for(String s : nextWords){
                    if(set.contains(s))
                        continue;
                    if(endWord.equals(s)){
                        return level;
                    }
                    q.offer(s);
                    set.add(s);
                }
            }            

        }
        return 0;
    }
}
```

还可以用two-end bfs，2个set代替queue。从两点端点一起走，比从单独一个端点走快。每次得到新层都用来替代start 的set

start始终要小，因为start一直在长大，每次还要loop start，所以尽量保持小。万一比end set就swap

终止条件是endword在end set里。

```text
class Solution {
    public int ladderLength(String beginWord, String endWord, List<String> wordList) {

            return bfs(beginWord, endWord, wordList);
    }

    List<String> getNextWord(String cur, Set
                             <String> wordList){
        List<String> ret = new ArrayList<String>();
        char[] cs = cur.toCharArray();
        for(int i = 0; i < cur.length(); i ++){                   
            for(char c = 'a' ; c <= 'z'; c ++){
                if(cs[i] == c){
                    continue;
                }                    
                char temp = cs[i];
                cs[i] = c;
                String nw = new String(cs);                
                if(wordList.contains(nw)){
                    ret.add(nw);
                }
                cs[i] = temp;
            }                
        } 
        return ret;
    }

    int bfs(String beginWord, String endWord, List<String> wordList){
        Set<String> visited = new HashSet<String>();
        Set<String> dict = new HashSet<>();
        for (String word : wordList) {
            dict.add(word);
        }
        if(!dict.contains(endWord))
            return 0;
        Set<String> start = new HashSet<String>();
        Set<String> end = new HashSet<String>();
        start.add(beginWord);
        end.add(endWord);
        int level = 1;

        while(!start.isEmpty() && !end.isEmpty()){
            //start始终要小，因为start一直在长大，每次还要loop start，所以尽量保持小。
            if(start.size() > end.size()){
               Set<String> temps = start;
                start = end;
                end = temps;
            }
            level ++;
            Set<String> temp = new HashSet<String>();
            for(String cur : start){
                List<String> nextWords = getNextWord(cur, dict);
                for(String s : nextWords){
                    if(end.contains(s)){//end段含有该数即可返回
                        return level;
                    }
                    if(visited.contains(s))
                        continue;

                    temp.add(s);
                    visited.add(s);
                }
            }            
           start = temp;             
        }
        return 0;
    }
}
```

Python

dict加了个set就过了

```text
import string


class Solution(object):
    def ladderLength(self, beginWord, endWord, wordList):
        """
        :type beginWord: str
        :type endWord: str
        :type wordList: List[str]
        :rtype: int
        """

        q = [beginWord]
        distance = {beginWord:1}
        wordList = set(wordList)
        while q:
            cur = q.pop(0)
            if cur == endWord:
                return distance[cur]
            nexts = self.getNext(cur,wordList)
            for n in nexts:
                if n not in distance:
                    distance[n] = distance[cur]+1
                    q.append(n)
        return 0





    def getNext(self,word,wordList):
        old = word
        res = []
        for pos in range(len(word)):
            temp = word[pos]            
            for i in string.ascii_lowercase:
                if i != temp:
                    word = word[:pos]+i+word[pos+1:]
                    if word in wordList:
                        res.append(str(word))
            word = old
        return res
```

