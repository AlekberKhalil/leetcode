# Implement Trie \(Prefix Tree\)

Implement a trie with`insert`,`search`, and`startsWith`methods.

**Example:**

```text
Trie trie = new Trie();

trie.insert("apple");
trie.search("apple");   // returns true
trie.search("app");     // returns false
trie.startsWith("app"); // returns true
trie.insert("app");   
trie.search("app");     // returns true
```

分析

prefix的话不用末尾has word ==true 只要能到底就好

iterative

```text
import collections

class TrieNode:
    def __init__(self,x):
        self.x = x
        self.children = collections.defaultdict(TrieNode)
        self.hasWord = False

class Trie:
    def __init__(self):
        """
        Initialize your data structure here.
        """
        self.root = TrieNode('')

    def insert(self, word):
        """
        Inserts a word into the trie.
        :type word: str
        :rtype: void
        """
        cur = self.root
        for c in word:
            if c not in cur.children:
                cur.children[c] = TrieNode(c)
            cur = cur.children.get(c)
        cur.hasWord = True



    def search(self, word):
        """
        Returns if the word is in the trie.
        :type word: str
        :rtype: bool
        """
        cur = self.root
        for c in word:
            if c not in cur.children:
                return False
            cur = cur.children.get(c)
        return cur.hasWord

    def startsWith(self, prefix):
        """
        Returns if there is any word in the trie that starts with the given prefix.
        :type prefix: str
        :rtype: bool
        """
        cur = self.root
        for c in prefix:
            if c not in cur.children:
                return False
            cur = cur.children.get(c)
        return True


# Your Trie object will be instantiated and called as such:
# obj = Trie()
# obj.insert(word)
# param_2 = obj.search(word)
# param_3 = obj.startsWith(prefix)
```

Recursive

递归在Trie里,对比前面Node里递归

```text
class TrieNode:
    def __init__(self,c):
        self.c = c
        self.children = {}
        self.hasWord = False
        
class Trie:

    def __init__(self):
        """
        Initialize your data structure here.
        """
        self.root = TrieNode('')
       

    def insert(self, word: str, pos = None, cur = None) -> None:
        """
        Inserts a word into the trie.
        """        
        pos = pos or 0
        cur = cur or self.root
        if pos == len(word):
            cur.hasWord = True #记得设置这块
            return
        if word[pos] not in cur.children:
            cur.children[word[pos]] = TrieNode(word[pos])
        self.insert(word, pos + 1, cur.children[word[pos]])
        

    def search(self, word: str, pos = None, cur = None) -> bool:
        """
        Returns if the word is in the trie.
        """
        pos = pos or 0
        cur = cur or self.root
        
        if pos == len(word):
            return cur.hasWord
        if word[pos] not in cur.children:
            return False
        return self.search(word, pos + 1, cur.children[word[pos]])
        
        

    def startsWith(self, prefix: str,  pos = None, cur = None) -> bool:
        """
        Returns if there is any word in the trie that starts with the given prefix.
        """
        pos = pos or 0
        cur = cur or self.root
        
        if pos == len(prefix): #prefix能到底就好，不需要判断Hasword
            return True
        if prefix[pos] not in cur.children:
            return False
        return self.startsWith(prefix, pos + 1, cur.children[prefix[pos]])
        
        


# Your Trie object will be instantiated and called as such:
# obj = Trie()
# obj.insert(word)
# param_2 = obj.search(word)
# param_3 = obj.startsWith(prefix)
```

