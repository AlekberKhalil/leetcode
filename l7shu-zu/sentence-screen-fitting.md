# Sentence Screen Fitting

Given a`rows x cols`screen and a sentence represented by a list of**non-empty**words, find**how many times**the given sentence can be fitted on the screen.

**Note:**

1. A word cannot be split into two lines.
2. The order of words in the sentence must remain unchanged.
3. Two consecutive words

   **in a line**

   must be separated by a single space.

4. Total words in the sentence won't exceed 100.
5. Length of each word is greater than 0 and won't exceed 10.
6. 1 ≤ rows, cols ≤ 20,000.

**Example 1:**

```text
Input:rows = 2, cols = 8, sentence = ["hello", "world"]Output:1Explanation:hello---world---The character '-' signifies an empty space on the screen.
```

**Example 2:**

```text
Input:rows = 3, cols = 6, sentence = ["a", "bcd", "e"]Output:2Explanation:a-bcd- e-a---bcd-e-The character '-' signifies an empty space on the screen.
```

**Example 3:**

```text
Input:rows = 4, cols = 5, sentence = ["I", "had", "apple", "pie"]Output:1Explanation:I-hadapplepie-Ihad--The character '-' signifies an empty space on the screen.
```

分析

start表示当前总放入字符数。 每次row直接start+= cols。 然后start%len是空格代表本行不需要Padding。 不是的话去掉最后单词。

```text
class Solution:    def wordsTyping(self, sentence: List[str], rows: int, cols: int) -> int:        s = ' '.join(sentence)+' '        ln = len(s)        start = 0        for i in range(rows):            start += cols            if s[start %ln] == ' ': #可以塞入当前row,不用padding                start += 1            else:#去掉最后一个word,去下一行                while start > 0 and s[(start-1)%ln] != ' ':#loop出来start在某word第一个字母处                    start -= 1        return  start//ln
```

