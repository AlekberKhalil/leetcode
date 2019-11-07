# Letter Combinations of a Phone Number\(dfs\)

Given a string containing digits from`2-9`inclusive, return all possible letter combinations that the number could represent.

A mapping of digit to letters \(just like on the telephone buttons\) is given below. Note that 1 does not map to any letters.

![](http://upload.wikimedia.org/wikipedia/commons/thumb/7/73/Telephone-keypad2.svg/200px-Telephone-keypad2.svg.png)

**Example:**

```text
Input: "23"Output: ["ad", "ae", "af", "bd", "be", "bf", "cd", "ce", "cf"].
```

分析：

dfs,lettermap可以用dict也可以array

```text
class Solution:    def letterCombinations(self, digits):        """        :type digits: str        :rtype: List[str]        """        if not digits:            return []        # lettermap = dict([('0',""),('1',""),('2',"abc"),('3',"def"),('4',"ghi"),('5',"jkl"),('6',"mno"),('7',"pqrs"),('8',"tuv"),('9',"wxyz")])        lettermap = ["","","abc","def","ghi","jkl","mno","pqrs","tuv","wxyz"]        ret=[]        self.dfs(digits,ret,"",0,lettermap)        return ret    def dfs(self,digits,ret,path,pos,lettermap):        if pos == len(digits):            ret.append(path)            return         for c in lettermap[int(digits[pos])]:            self.dfs(digits,ret,path+c,pos+1,lettermap)
```

