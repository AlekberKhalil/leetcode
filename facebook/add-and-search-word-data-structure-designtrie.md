# Add and Search Word - Data structure design（Trie\)

Design a data structure that supports the following two operations:

```text
void addWord(word)bool search(word)
```

search\(word\) can search a literal word or a regular expression string containing only letters`a-z`or`.`. A`.`means it can represent any one letter.

**Example:**

```text
addWord("bad")addWord("dad")addWord("mad")search("pad") -> falsesearch("bad") -> truesearch(".ad") -> truesearch("b..") -> true
```

**Note:**  
You may assume that all words are consist of lowercase letters`a-z`.

分析

Trie用递归

```text
import collectionsimport stringclass TrieNode:    def __init__(self,c):        self.c = c        self.children = collections.defaultdict(TrieNode)        self.hasWord = Falseclass WordDictionary:    LETTERS = list(string.ascii_lowercase)    def __init__(self):        """        Initialize your data structure here.        """        self.trie = TrieNode('')    def addWord(self, word):        """        Adds a word into the data structure.        :type word: str        :rtype: void        """        self.insert(self.trie,word,0)    def insert(self,trieNode,word,pos):        if pos == len(word):            trieNode.hasWord = True            return        if word[pos] != '.':            if word[pos] not in trieNode.children:                trieNode.children[word[pos]] = TrieNode(word[pos])            self.insert(trieNode.children.get(word[pos]),word,pos+1)        else:            for c in self.LETTERS:                if c not in trieNode.children:                    trieNode.children[c] = TrieNode(c)                self.insert(trieNode.children.get(c), word, pos + 1)    def search(self, word):        """        Returns if the word is in the data structure. A word could contain the dot character '.' to represent any one letter.        :type word: str        :rtype: bool        """        return self.exist(self.trie,word,0)    def exist(self, trieNode, word, pos):        if pos == len(word):            return trieNode.hasWord        if word[pos] != '.':            return word[pos] in trieNode.children and self.exist(trieNode.children.get(word[pos]), word, pos + 1)        else:            res = False            for c in self.LETTERS:                if c in trieNode.children and self.exist(trieNode.children.get(c), word, pos + 1):                    res = True                    break        return res# Your WordDictionary object will be instantiated and called as such:# obj = WordDictionary()# obj.addWord(word)# param_2 = obj.search(word)
```

忘了Insert不必考虑.的情况

```text
import collectionsimport stringclass TrieNode:    def __init__(self, c):        self.c = c        self.children = collections.defaultdict(TrieNode)        self.hasWord = Falseclass WordDictionary:    LETTERS = list(string.ascii_lowercase)    def __init__(self):        """        Initialize your data structure here.        """        self.trie = TrieNode('')    def addWord(self, word):        """        Adds a word into the data structure.        :type word: str        :rtype: void        """        cur = self.trie        for c in word:            if c not in cur.children:                cur.children[c] = TrieNode(c)            cur = cur.children.get(c)        cur.hasWord = True        # self.insert(self.trie, word, 0)    def insert(self, trieNode, word, pos):        if pos == len(word):            trieNode.hasWord = True            return        if word[pos] != '.':            if word[pos] not in trieNode.children:                trieNode.children[word[pos]] = TrieNode(word[pos])            self.insert(trieNode.children.get(word[pos]), word, pos + 1)        else:            for c in self.LETTERS:                if c not in trieNode.children:                    trieNode.children[c] = TrieNode(c)                self.insert(trieNode.children.get(c), word, pos + 1)    def search(self, word):        """        Returns if the word is in the data structure. A word could contain the dot character '.' to represent any one letter.        :type word: str        :rtype: bool        """        return self.exist(self.trie, word, 0)    def exist(self, trieNode, word, pos):        if pos == len(word):            return trieNode.hasWord        if word[pos] != '.':            return word[pos] in trieNode.children and self.exist(trieNode.children.get(word[pos]), word, pos + 1)        else:            res = False            for c in self.LETTERS:                if c in trieNode.children and self.exist(trieNode.children.get(c), word, pos + 1):                    res = True                    break        return res# Your WordDictionary object will be instantiated and called as such:# obj = WordDictionary()# obj.addWord(word)# param_2 = obj.search(word)
```

