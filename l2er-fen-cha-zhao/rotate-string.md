# Rotate String

Given a string and an offset, rotate string by offset. \(rotate from left to right\)

Have you met this question in a real interview?

Yes

**Example**

Given`"abcdefg"`.

```text
offset=0 => "abcdefg"
offset=1 => "gabcdef"
offset=2 => "fgabcde"
offset=3 => "efgabcd"
```

分析

三步翻转，先总体，再每个单词, offsert需要%

```text
public class Solution {
    /**
     * @param str: an array of char
     * @param offset: an integer
     * @return: nothing
     */
    public void rotateString(char[] str, int offset) {

        if(str == null || str.length == 0)
            return;
        if(offset > str.length){
            offset = offset % str.length;
        }

        reverse(str, 0, str.length - 1);
        reverse(str, 0, offset - 1);
        reverse(str, offset, str.length - 1);
    }

        public void reverse(char[] str, int s, int e){
        while(s < e){
            char temp = str[s];
            str[s++] = str[e];
            str[e--] = temp;
        }

    }
    //     helper(str, 0, str.length - 1 - offset);
    //     helper(str, str.length - offset, str.length - 1);

    //     helper(str, 0 , str.length - 1);
    // }

    // private char[] helper(char[] cs, int ss, int e){
    //     while(ss < e){
    //         char temp = cs[ss];
    //         cs[ss] = cs[e];
    //         cs[e] = temp;
    //         ss ++;
    //         e --;
    //     }
    //     return cs;
    // }
    //     // write your code here
    //     if (str == null || str.length == 0)
    //         return;

    //     int n = str.length;
    //     offset = offset % str.length;
    //     reverse(str, 0, n - offset - 1);
    //     reverse(str, n - offset, n-1);
    //     reverse(str, 0, n-1);
    // }

}
```

