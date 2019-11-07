# Implement Trie

Implement a trie with insert, search, and startsWith methods.

## Notice

You may assume that all inputs are consist of lowercase letters a-z.

**Example**

```text
insert("lintcode")search("code") >>> falsestartsWith("lint")>>> truestartsWith("linterror")>>> falseinsert("linterror")search("lintcode)>>> truestartsWith("linterror")>>> true
```

分析：

一个单词就是一棵树下来，每个node有26个字母可做孩子。

注意点：1 用数组表示children 2 TrieNode里定义了所有函数，返回node 3 hasWord在insert里set，在find里不用，因为直接返回了node

除了数组还可以用hashmap

答案：

初始化时cur = root,然后往下loop word.length,最后到达最后一个node。

```text
/** * Your Trie object will be instantiated and called as such: * Trie trie = new Trie(); * trie.insert("lintcode"); * trie.search("lint"); will return false * trie.startsWith("lint"); will return true */class TrieNode {    // Initialize your data structure here.    public TrieNode[] children;    public boolean hasWord;    public TrieNode() {        children = new TrieNode[26];        hasWord = false;    }    //  public void insert(String word, int index) {    //     if(index == word.length()){    //         hasWord = true;    //         return;    //     }    //     int pos = word.charAt(index) - 'a';    //     if(children[pos] == null){    //         children[pos] = new TrieNode();    //     }    //     children[pos].insert(word, index+1);    // }    // public TrieNode find(String word, int index) {    //     if(index == word.length()){    //         return this;    //     }    //     int pos = word.charAt(index) - 'a';    //     if (children[pos] == null) {    //         return null;    //     }    //     return children[pos].find(word, index+1);    // }    public void insert(String word) {        TrieNode cur = this;        for(int i = 0;  i < word.length(); i ++){             int pos = word.charAt(i) - 'a';            if(cur.children[pos] == null){                cur.children[pos] = new TrieNode();            }            cur = cur.children[pos];        }        cur.hasWord = true;    }    public TrieNode find(String word) {        TrieNode cur = this;        for(int i = 0;  i < word.length(); i ++){             int pos = word.charAt(i) - 'a';            if(cur.children[pos] == null){                return null;            }            cur = cur.children[pos];        }        return cur;    }}public class Trie {    private TrieNode root;    public Trie() {        root = new TrieNode();    }    // Inserts a word into the trie.    public void insert(String word) {        root.insert(word);    }    // Returns if the word is in the trie.    public boolean search(String word) {         TrieNode cur = root.find(word);         return cur!= null && cur.hasWord;    }    // Returns if there is any word in the trie    // that starts with the given prefix.    public boolean startsWith(String prefix) {        TrieNode cur = root.find(prefix);         return cur!= null;    }}
```

```text
/** * Your Trie object will be instantiated and called as such: * Trie trie = new Trie(); * trie.insert("lintcode"); * trie.search("lint"); will return false * trie.startsWith("lint"); will return true */class TrieNode {    // Initialize your data structure here.    private TrieNode[] children;    public boolean hasWord;    public TrieNode() {        children = new TrieNode[26];        hasWord = false;    }     public void insert(String word, int index) {        if(index == word.length()){            hasWord = true;            return;        }        int pos = word.charAt(index) - 'a';        if(children[pos] == null){            children[pos] = new TrieNode();        }        children[pos].insert(word, index+1);    }    public TrieNode find(String word, int index) {        if(index == word.length()){            return this;        }        int pos = word.charAt(index) - 'a';        if (children[pos] == null) {            return null;        }        return children[pos].find(word, index+1);    }}public class Trie {    private TrieNode root;    public Trie() {        root = new TrieNode();    }    // Inserts a word into the trie.    public void insert(String word) {        root.insert(word, 0);    }    // Returns if the word is in the trie.    public boolean search(String word) {        TrieNode t = root.find(word, 0);        return t!= null && t.hasWord;    }    // Returns if there is any word in the trie    // that starts with the given prefix.    public boolean startsWith(String prefix) {        TrieNode t = root.find(prefix, 0);        return t!= null;    }}
```

hashmap实现法

```text
class Trie {    TrieNode root;    /** Initialize your data structure here. */    public Trie() {        root = new TrieNode();    }    /** Inserts a word into the trie. */    public void insert(String word) {        HashMap<Character, TrieNode> curChildren = root.children;        char[] cs = word.toCharArray();        for(int i = 0; i < cs.length; i ++){            char c = cs[i];            if(!curChildren.containsKey(c)){                curChildren.put(c, new TrieNode());            }            TrieNode cur = curChildren.get(c);            curChildren = cur.children;            if(i == cs.length-1){                cur.hasWord = true;            }        }    }    /** Returns if the word is in the trie. */    public boolean search(String word) {        TrieNode n = find(word);        return n != null && n.hasWord;    }    /** Returns if there is any word in the trie that starts with the given prefix. */    public boolean startsWith(String prefix) {        TrieNode n = find(prefix);        return n != null;    }    public TrieNode find(String word){          HashMap<Character, TrieNode> curChildren = root.children;        char[] cs = word.toCharArray();        for(int i = 0; i < cs.length; i ++){            char c = cs[i];            if(!curChildren.containsKey(c)){                return null;            }            TrieNode cur = curChildren.get(c);            curChildren = cur.children;            if(i == cs.length-1){                return cur;            }        }        return null;    }}class TrieNode {    char c;    boolean hasWord;    HashMap<Character, TrieNode> children = new HashMap<Character, TrieNode>();    public TrieNode(){    }    public TrieNode(char c){        this.c = c;    } }/** * Your Trie object will be instantiated and called as such: * Trie obj = new Trie(); * obj.insert(word); * boolean param_2 = obj.search(word); * boolean param_3 = obj.startsWith(prefix); */
```

