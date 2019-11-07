# Decode String

Given an encoded string, return it's decoded string.

The encoding rule is:`k[encoded_string]`, where theencoded\_stringinside the square brackets is being repeated exactlyktimes. Note thatkis guaranteed to be a positive integer.

You may assume that the input string is always valid; No extra white spaces, square brackets are well-formed, etc.

Furthermore, you may assume that the original data does not contain any digits and that digits are only for those repeat numbers,k. For example, there won't be input like`3a`or`2[4]`.

**Examples:**

```text
s = "3[a]2[bc]", return "aaabcbc".s = "3[a2[c]]", return "accaccacc".s = "2[abc]3[cd]ef", return "abcabccdcdcdef".
```

分析

递归，主循环里分别判断isDigit, isLetter和"\]"

isDigit 得到数字并且跳过\[，递归得到子字符串，然后循环加入结果

isletter 相加得到字符串

\] 退出该次循环，返回结果

注意这里i用int\[\]来得到i的引用，否则主程序里无法得到更新的i继续

用stingbuilder来提高效率

```text
class Solution {    public String decodeString(String s) {        StringBuilder str = new StringBuilder(s);//空间效率        int[] i = new int[1];//传引用        i[0] = 0;        return decodeString(s, i);    }    String decodeString(StringBuilder s, int[] i){        // && s.charAt(i[0]) != ']'        // int n = 0;        StringBuilder ret = new StringBuilder();        while(i[0] < s.length()){            if(Character.isLetter(s.charAt(i[0]))){                ret.append(s.charAt(i[0] ++));            }else if(Character.isDigit(s.charAt(i[0]))){                int n = 0;                while(Character.isDigit(s.charAt(i[0]))){                    n = n * 10 + s.charAt(i[0] ++) - '0';//不是+=这里                }                                                             i[0] ++; //"["                String ds = decodeString(s, i);                while(n -- > 0){                      ret.append(ds);                    }            }else if(s.charAt(i[0]) == ']'){                i[0] ++;                return ret.toString();            }        }          return ret.toString();   }              }
```

用栈，数字栈和字母栈

数字时，入数字栈

字母时，累加得到res

\[ 字母res入栈

\] 数字字母出栈，得到新res，新res不要在此处入栈！！！！！

```text
class Solution {    public String decodeString(String s) {        Stack<Integer> cnt = new Stack<Integer>();        Stack<String> str = new Stack<String>();        String res = new String();        int idx = 0;        while(idx < s.length()){            if(Character.isDigit(s.charAt(idx))){//数字入栈                int n = 0;                while(Character.isDigit(s.charAt(idx))){                    n = n * 10 + s.charAt(idx ++) - '0';                }                cnt.push(n);            }else if(s.charAt(idx) == '['){ //字母入栈                str.push(res);                res = "";                idx ++;            }else if(s.charAt(idx) == ']'){//出栈                StringBuilder temp = new StringBuilder(str.pop());                int time = cnt.pop();                while(time -- > 0){                    temp.append(res);   //这里append 还是用stringbuilder                                 }                res = temp.toString();//关键步骤，此处更新res就好，不必加入stack，让'['时处理                idx ++;            }else{                res += s.charAt(idx ++); //可以直接char相加得到string            }        }        return res;    }}
```

