# Text Justification



Given an array of words and a width _maxWidth_, format the text such that each line has exactly _maxWidth_ characters and is fully \(left and right\) justified.

You should pack your words in a greedy approach; that is, pack as many words as you can in each line. Pad extra spaces `' '` when necessary so that each line has exactly _maxWidth_ characters.

Extra spaces between words should be distributed as evenly as possible. If the number of spaces on a line do not divide evenly between words, the empty slots on the left will be assigned more spaces than the slots on the right.

For the last line of text, it should be left justified and no **extra** space is inserted between words.

**Note:**

* A word is defined as a character sequence consisting of non-space characters only.
* Each word's length is guaranteed to be greater than 0 and not exceed _maxWidth_.
* The input array `words` contains at least one word.

**Example 1:**

```text
Input:
words = ["This", "is", "an", "example", "of", "text", "justification."]
maxWidth = 16
Output:
[
   "This    is    an",
   "example  of text",
   "justification.  "
]
```

**Example 2:**

```text
Input:
words = ["What","must","be","acknowledgment","shall","be"]
maxWidth = 16
Output:
[
  "What   must   be",
  "acknowledgment  ",
  "shall be        "
]
Explanation: Note that the last line is "shall be    " instead of "shall     be",
             because the last line must be left-justified instead of fully-justified.
             Note that the second line is also left-justified becase it contains only one word.
```

**Example 3:**

```text
Input:
words = ["Science","is","what","we","understand","well","enough","to","explain",
         "to","a","computer.","Art","is","everything","else","we","do"]
maxWidth = 20
Output:
[
  "Science  is  what we",
  "understand      well",
  "enough to explain to",
  "a  computer.  Art is",
  "everything  else  we",
  "do                  "
]

```

分析

{% embed url="https://leetcode.com/problems/text-justification/discuss/24891/Concise-python-solution-10-lines." %}

round robin ,只填中间的gap，所以是gapNum-1 = len\(word\)-2,最右不填，除非只有一个word时候，全部塞右边。注意i%j，分布在j-1中

cur 纯单词list，每次找出某个w后面 w+=’ ‘

letterLen, 纯单词长度无添加。

加入res的是cur=》str

最后返回结果，要考虑最后cur需要做ljust再加入res



```text
for j in range(maxWidth-letterLen):
    cur[j%(len(cur)-1 or 1)] +=' ' #cur
```

```text
class Solution:
    def fullJustify(self, words: List[str], maxWidth: int) -> List[str]:
        cur,letterLen,res = [],0,[]
        for w in words:
            if letterLen + len(cur) + len(w) >maxWidth:
                for j in range(maxWidth-letterLen):
                    cur[j%(len(cur)-1 or 1)] +=' '
                res.append(''.join(cur))
                cur, letterLen = [], 0
            cur += [w]
            letterLen += len(w)
        return res +[' '.join(cur).ljust(maxWidth)]
```

