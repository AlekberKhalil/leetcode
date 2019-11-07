# Prefix and Suffix Search\(Trie\)

Given many`words`,`words[i]`has weight`i`.

Design a class`WordFilter`that supports one function,`WordFilter.f(String prefix, String suffix)`. It will return the word with given`prefix`and`suffix`with maximum weight. If no word exists, return -1.

**Examples:**

```text
Input:WordFilter(["apple"])WordFilter.f("a", "e") // returns 0WordFilter.f("b", "") // returns -1
```

Note:

```text
words has length in range [1, 15000].For each test case, up to words.length queries WordFilter.f may be made.words[i] has length in range [1, 10].prefix, suffix have lengths in range [0, 10].words[i] and prefix, suffix queries consist of lowercase letters only.
```

分析

1 建2个树，然后pre找pre树，suffix找suffix树，这里倒建倒查。容易超时。

2.insert`'#apple', 'e#apple', 'le#apple', 'ple#apple', 'pple#apple', 'apple#apple'`

into the trie. Then for a query like`prefix = "ap", suffix = "le"`, we can find it by querying our trie for`le#ap`

注意这里weight， 因为w是word的index，所以树里一个Node的w虽然一直被更新，但最新的w就是最后那个word的index,也就是最大的。

```text
class WordFilter {    TrieNode root ;    public WordFilter(String[] words) {        root = new TrieNode();        //建树        for(int w = 0; w < words.length; w ++){            String word = words[w] + "{";            for(int i = 0; i < word.length(); i ++){                //算起来这里才是每个word开始的地方，所以这里开始初始cur。                TrieNode cur = root;                cur.w = w;//每个word得到最新的weight，就是当前的Index.                for(int j = i; j < 2 * word.length() - 1; j ++){                    int pos = word.charAt(j % word.length()) - 'a';                    if(cur.child[pos] == null) {                        cur.child[pos] = new TrieNode();                    }                    cur = cur.child[pos];                    cur.w = w;                }            }        }    }    public int f(String prefix, String suffix) {        String word = suffix+'{'+prefix;        TrieNode cur = root;        int ret = -1;        for(int i = 0; i < word.length(); i ++){            int pos = word.charAt(i) - 'a';            if(cur.child[pos] == null) {                return -1;            }            cur = cur.child[pos];        }    return cur.w;    }    class TrieNode{        TrieNode[] child;        int w;        TrieNode(){            this.child = new TrieNode[27];            this.w = 0;        }    }}/** * Your WordFilter object will be instantiated and called as such: * WordFilter obj = new WordFilter(words); * int param_1 = obj.f(prefix,suffix); */
```

.Python

python children里存的是dict\[c\] = TrieNode\(\) java是dict\[index\]一定要区别清楚

所以这里直接word是 w+\#+w 然后遍历整个word， 每个char dict\[char\]

```text
class TrieNode:    def __init__(self):        self.children = dict()        self.w = 0class WordFilter:    def __init__(self, words):        self.trie = TrieNode()        for i,w in enumerate(words):            w = w+"#"+w            for index in range(len(w)):                self.appendWord(index,w,i)    def appendWord(self, i, word, weight):        cur = self.trie        for j in word[i:]:            child = cur.children.get(j)            if not child:                child = TrieNode()                child.w = weight                cur.children[j] = child            cur = child    def f(self, prefix, suffix):        w = suffix+"#"+prefix        cur = self.trie        for c in w:            if cur: cur = cur.children.get(c)        return cur.wobj = WordFilter(["apple", "island","ironman", "i love leetcode"])param_1 = obj.f("i","d")print(param_1)
```

