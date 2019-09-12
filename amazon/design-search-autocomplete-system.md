# Design Search Autocomplete System



Design a search autocomplete system for a search engine. Users may input a sentence \(at least one word and end with a special character `'#'`\). For **each character** they type **except '\#'**, you need to return the **top 3** historical hot sentences that have prefix the same as the part of sentence already typed. Here are the specific rules:

1. The hot degree for a sentence is defined as the number of times a user typed the exactly same sentence before.
2. The returned top 3 hot sentences should be sorted by hot degree \(The first is the hottest one\). If several sentences have the same degree of hot, you need to use ASCII-code order \(smaller one appears first\).
3. If less than 3 hot sentences exist, then just return as many as you can.
4. When the input is a special character, it means the sentence ends, and in this case, you need to return an empty list.

Your job is to implement the following functions:

The constructor function:

`AutocompleteSystem(String[] sentences, int[] times):` This is the constructor. The input is **historical data**. `Sentences` is a string array consists of previously typed sentences. `Times` is the corresponding times a sentence has been typed. Your system should record these historical data.

Now, the user wants to input a new sentence. The following function will provide the next character the user types:

`List<String> input(char c):` The input `c` is the next character typed by the user. The character will only be lower-case letters \(`'a'` to `'z'`\), blank space \(`' '`\) or a special character \(`'#'`\). Also, the previously typed sentence should be recorded in your system. The output will be the **top 3** historical hot sentences that have prefix the same as the part of sentence already typed. 

**Example:**  
**Operation:** AutocompleteSystem\(\["i love you", "island","ironman", "i love leetcode"\], \[5,3,2,2\]\)  
The system have already tracked down the following sentences and their corresponding times:  
`"i love you"` : `5` times  
`"island"` : `3` times  
`"ironman"` : `2` times  
`"i love leetcode"` : `2` times  
Now, the user begins another search:  
  
**Operation:** input\('i'\)  
**Output:** \["i love you", "island","i love leetcode"\]  
**Explanation:**  
There are four sentences that have prefix `"i"`. Among them, "ironman" and "i love leetcode" have same hot degree. Since `' '` has ASCII code 32 and `'r'` has ASCII code 114, "i love leetcode" should be in front of "ironman". Also we only need to output top 3 hot sentences, so "ironman" will be ignored.  
  
**Operation:** input\(' '\)  
**Output:** \["i love you","i love leetcode"\]  
**Explanation:**  
There are only two sentences that have prefix `"i "`.  
  
**Operation:** input\('a'\)  
**Output:** \[\]  
**Explanation:**  
There are no sentences that have prefix `"i a"`.  
  
**Operation:** input\('\#'\)  
**Output:** \[\]  
**Explanation:**  
The user finished the input, the sentence `"i a"` should be saved as a historical sentence in system. And the following input will be counted as a new search. 

**Note:**

1. The input sentence will always start with a letter and end with '\#', and only one blank space will exist between two words.
2. The number of **complete sentences** that to be searched won't exceed 100. The length of each sentence including those in the historical data won't exceed 100.
3. Please use double-quote instead of single-quote when you write test cases even for a character input.
4. Please remember to **RESET** your class variables declared in class AutocompleteSystem, as static/class variables are **persisted across multiple test cases**. Please see [here](https://leetcode.com/faq/#different-output) for more details.

分析

Trie里每个Node都带一个set的词语，走到那个Node就能返回一串list。 去map里找freq然后排序输出。

Trie里一个curNode记录当前走到的node， find这里改成每次只走一个char

Autocomplete System里curWord记录当前走的char。

排序用key = lambda x: \(-x\[0\],x\[1\]\)。先拍freq再排string

```text
class Node:
    def __init__(self, c):
        self.c = c
        self.words = set() #去重复word
        self.children = {}
        self.hasWord =False

class Trie:
    def __init__(self):
        self.root = Node('')
        self.curNode = self.root
    
    def insert(self, word):
        cur = self.root
        for w in word:
            if w not in cur.children:
                n = Node(w)
                cur.children[w] = n
            cur.children[w].words.add(word) #已经存在的话也要加word
            cur = cur.children[w]
        cur.hasWord = True
        cur.words.add(word) #走到最后也要加入word
    
    def find(self, c):     
        if not self.curNode:#起头就不对的word直接返回
            return []
        if c not in self.curNode.children:
            self.curNode = None #设置flag，开始就不对的话 将来也不必往下走了。否则会从头起
            return []
        self.curNode = self.curNode.children[c]
        return self.curNode.words
                                
class AutocompleteSystem:

    def __init__(self, sentences: List[str], times: List[int]):
        self.wordFreq = dict(zip(sentences,times))
        self.curWord = ''
        self.trie = Trie()
        for s in sentences:
            self.trie.insert(s)
        #self.trie.curNode = self.trie.root

    def input(self, c: str) -> List[str]:
        if c == '#':
            if self.curWord in self.wordFreq:
                self.wordFreq[self.curWord] += 1
            else:
                self.wordFreq[self.curWord] = 1
                self.trie.insert(self.curWord)
            self.curWord = ''
            self.trie.curNode = self.trie.root
            return []
        else:
            self.curWord += c
            wl = list(self.trie.find(c))
            tl = sorted([(self.wordFreq[w],w) for w in wl], key = lambda x: (-x[0],x[1]))
            
            
            return [x[1] for x in tl[:3]]
            
            
        
        


# Your AutocompleteSystem object will be instantiated and called as such:
# obj = AutocompleteSystem(sentences, times)
# param_1 = obj.input(c)
```



