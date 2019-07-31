# Add and Search Word

Design a data structure that supports the following two operations:`addWord(word)`and`search(word)`

`search(word)`can search a literal word or a regular expression string containing only letters`a-z`or`.`.

A`.`means it can represent any one letter.

**Example**

```text
addWord("bad")
addWord("dad")
addWord("mad")
search("pad")  // return false
search("bad")  // return true
search(".ad")  // return true
search("b..")  // return true
```

分析：

Trie树，因为有. child用数组可以得到下标，然后dfs做。 TrieNode class位置随便

答案：

```text
class TrieNode {
    public TrieNode[] children;
    public boolean hasWord;

    public TrieNode() {
        children = new TrieNode[26];
        for (int i = 0; i < 26; ++i)
            children[i] = null;
        hasWord = false;
    }
}

public class WordDictionary {
    TrieNode root = new TrieNode();
    // Adds a word into the data structure.
    public void addWord(String word) {
        // Write your code here
        TrieNode cur = root;
        char[] cs = word.toCharArray();
        for(int i = 0; i < cs.length; i++){
            if(cur.children[cs[i]-'a'] == null){
                cur.children[cs[i]-'a'] =  new TrieNode();
            }
            cur = cur.children[cs[i]-'a'];
        }
        cur.hasWord = true;
    }

    // Returns if the word is in the data structure. A word could
    // contain the dot character '.' to represent any one letter.
    public boolean search(String word) {
        // Write your code here
        return find(word, 0, root);

    }

     public boolean find(String word, int index, TrieNode cur){
        if(index == word.length())
            return cur.hasWord;

        if(word.charAt(index) == '.'){
            for(int j = 0; j < 26; j ++){
                if(cur.children[j] != null)
                   if(find(word, index + 1, cur.children[j])) 
                    return true;
            }
            return false;
        }
        else if(cur.children[word.charAt(index)-'a'] != null){
            return find(word, index + 1, cur.children[word.charAt(index)-'a']);
        }
             return false;
    }
}






// Your WordDictionary object will be instantiated and called as such:
// WordDictionary wordDictionary = new WordDictionary();
// wordDictionary.addWord("word");
// wordDictionary.search("pattern");
```

