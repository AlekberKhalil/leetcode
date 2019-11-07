# Rotate String

Given a string and an offset, rotate string by offset. \(rotate from left to right\)

**Example**

Given`"abcdefg"`.

```text
offset=0 => "abcdefg"
offset=1 => "gabcdef"
offset=2 => "fgabcde"
offset=3 => "efgabcd"
```

分析

参见前题的手翻转例子，先局部再整体翻转，注意char\[\]处理后直接用。同时offset记得判断。

答案

```text
    public void rotateString(char[] str, int offset) {
        if(str == null || str.length == 0)
            return;
        if(offset > str.length){
            offset = offset % str.length;
        }
        helper(str, 0, str.length - 1 - offset);
        helper(str, str.length - offset, str.length - 1);

        helper(str, 0 , str.length - 1);
    }

    private char[] helper(char[] cs, int ss, int e){
        while(ss < e){
            char temp = cs[ss];
            cs[ss] = cs[e];
            cs[e] = temp;
            ss ++;
            e --;
        }
        return cs;
    }
```

