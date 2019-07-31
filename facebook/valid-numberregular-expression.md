# valid number\(regular expression\)

Validate if a given string can be interpreted as a decimal number.

Some examples:  
`"0"`=&gt;`true`  
`" 0.1 "`=&gt;`true`  
`"abc"`=&gt;`false`  
`"1 a"`=&gt;`false`  
`"2e10"`=&gt;`true`  
`" -90e3 "`=&gt;`true`  
`" 1e"`=&gt;`false`  
`"e3"`=&gt;`false`  
`" 6e-1"`=&gt;`true`  
`" 99e2.5 "`=&gt;`false`  
`"53.5e93"`=&gt;`true`  
`" --6 "`=&gt;`false`  
`"-+3"`=&gt;`false`  
`"95a54e53"`=&gt;`false`

**Note:**It is intended for the problem statement to be ambiguous. You should gather all requirements up front before implementing one. However, here is a list of characters that can be in a valid decimal number:

* Numbers 0-9
* Exponent - "e"
* Positive/negative sign - "+"/"-"
* Decimal point - "."

Of course, the context of these characters also matters in the input.

分析

1. 空格 ‘ ’： 空格分为两种情况需要考虑，一种是出现在开头和末尾的空格，一种是出现在中间的字符。出现在开头和末尾的空格不影响数字，而一旦中间出现了空格，则立马不是数字。解决方法：预处理时去掉字符的首位空格，中间再检测到空格，则判定不是数字。
2. 小数点 '.'：小数点需要分的情况较多，首先的是小数点只能出现一次，但是小数点可以出现在任何位置，开头\(".3"\), 中间\("1.e2"\), 以及结尾\("1." \), 而且需要注意的是，小数点不能出现在自然数 'e/E' 之后，如 "1e.1" false, "1e1.1" false。还有，当小数点位于末尾时，前面必须是数字，如 "1." true，" -." false。解决方法：开头中间结尾三个位置分开讨论情况。
3. 自然数 'e/E'：自然数的前后必须有数字，即自然数不能出现在开头和结尾，如 "e" false, ".e1" false, "3.e" false, "3.e1" true。而且小数点只能出现在自然数之前，还有就是自然数前面不能是符号，如 "+e1" false, "1+e" false. 解决方法：开头中间结尾三个位置分开讨论情况。
4. 正负号 '+/-"，正负号可以再开头出现，可以再自然数e之后出现，但不能是最后一个字符，后面得有数字，如 "**+1.e+5**" true。解决方法：开头中间结尾三个位置分开讨论情况。

对于'e'，最多只允许出现1次，其前后都必须有数字，但后面一定是整数，即不能出现'.'；

引自百度：3.2e10是计算器显示的结果.是显示的科学计数法,e代表的意思是x10的n次方,也就是3.2X10的10次方.

.e+

{min,max}

re.compile\('regex'\).search\(s\) is not None

\(\)? \[\]?

```text
import re


class Solution:
    def isNumber(self, s):
        """
        :type s: str
        :rtype: bool
        """
        return s.count('.')<=1 and re.compile('^\s*[+-]?[0-9\.]{'+str(s.count('.')+1)+',}(e[+-]?[0-9]+)?\s*$').search(s) is not None
```

