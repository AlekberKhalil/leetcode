# Rotate String

题目

Given a string and an offset, rotate string by offset. \(rotate from left to right\)

**Example**

Given`"abcdefg"`.

```text
offset=0 => "abcdefg"
offset=1 =>"gabcdef"
offset=2 => "fgabcde"
offset=3 => "efgabcd"
```

分析：

也是三步翻转法，记得offset可能超过数组大小，记得取模。

解法：

```text
    public void rotateString(char[] str, int offset) {
        // 判断非空和长度xxx
        if (str == null || str.length == 0)
            return;

        int n = str.length;
        offset = offset % str.length;//注意Offset要取模xxx
        reverse(str, 0, n - offset - 1);
        reverse(str, n - offset, n-1);
        reverse(str, 0, n-1);
    }

    public void reverse(char[] str, int s, int e){
        while(s < e){
            char temp = str[s];
            str[s++] = str[e];
            str[e--] = temp;
        }

    }
```

