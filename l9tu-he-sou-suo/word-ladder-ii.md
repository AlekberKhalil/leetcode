# Word Ladder II

Given two words \(beginWordandendWord\), and a dictionary's word list, find all shortest transformation sequence\(s\) frombeginWordtoendWord, such that:

1. Only one letter can be changed at a time
2. Each transformed word must exist in the word list. Note tha beginWord is not a transformed word.

For example,

Given:  
beginWord=`"hit"`  
endWord=`"cog"`  
wordList=`["hot","dot","dog","lot","log","cog"]`

Return

```text
  [
    ["hit","hot","dot","dog","cog"],
    ["hit","hot","lot","log","cog"]
  ]
```

分析

* BFS得到所有最短路径， DFS遍历输出
* BFS 其中用map father保存路径，用字典里所有words做key，然后存储所有可到word的father点，father放在list里。
* Distance用法妙极，在BFS里可以判重，在DFS里判断最短路径。
* BFS里第一次遇到的word直接存入distance里，因为将来再遇到只会路径只会更长。同时也用来判重，再者distance不像father里所有字典里的word都在father的keyset里。distance里不一定包含字典里所有words，因为word不一定可达。
* DFS里Collections.reverse\(List l\)

```text
class Solution {
    Map<String,List<String>> father = new HashMap<String,List<String>>();
    Map<String, Integer> distance = new HashMap<String, Integer>();

    public List<List<String>> findLadders(String beginWord, String endWord, List<String> wordList) {
        List<List<String>> ret = new ArrayList<>();
        if(!wordList.contains(endWord))
            return ret;

        List<String> path = new ArrayList<String>();
        wordList.add(beginWord);
        // wordList.add(endWord);
        bfs(beginWord, endWord, wordList);
        dfs(ret, path, endWord, beginWord);
        return ret;
    }
    void dfs(List<List<String>> ret, List<String> path, String s, String e){
        path.add(s);
        if(s.equals(e)){
            List<String> nl = new ArrayList<String>(path);
            Collections.reverse(nl);
            ret.add(nl);
        }else{
            for(String f : father.get(s)){
                //distance来找到合适的father。
                if(distance.containsKey(f) && distance.get(s) == distance.get(f) + 1){
                    dfs(ret, path, f, e);
                }
            }

        }
        path.remove(path.size() - 1);
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

    void bfs(String beginWord, String endWord, List<String> wordList){
        Queue<String> q = new LinkedList<String>();
        //用set存字典，为了让查contains更快
        Set<String> dict = new HashSet<>();        
        for (String word : wordList) {
            father.put(word, new ArrayList<String>());
            dict.add(word);
        }
        q.add(beginWord);
        distance.put(beginWord, 0);

        while(!q.isEmpty()){          
            String cur = q.poll();
            List<String> nextWords = getNextWord(cur, dict);
            for(String s : nextWords){
                father.get(s).add(cur);//新的word都是在字典里的，所以father不必判断，可以得到所有情况
                if(!distance.containsKey(s)){//字典里并非所有字母都可达，所以需要判断，这里也是为了去重。
                   distance.put(s, distance.get(cur) + 1);//第一个到的就是最短的，后来的不要再加了，会越来越大的。
                    q.offer(s); 
                }

            }
        }

    }
}
```

