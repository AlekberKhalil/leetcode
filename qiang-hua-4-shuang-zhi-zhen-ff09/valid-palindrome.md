# Valid Palindrome

Given a string, determine if it is a palindrome, considering only alphanumeric characters and ignoring cases.

## Notice

Have you consider that the string might be empty? This is a good question to ask during an interview.

For the purpose of this problem, we define empty string as valid palindrome.

**Example**

`"A man, a plan, a canal: Panama"`is a palindrome.

`"race a car"`is not a palindrome.

分析

对撞指针。此题重点如何判断数字和字母。

大while里的小while，小while需要判断边界

答案

```text
public class Solution {
    /*
     * @param s: A string
     * @return: Whether the string is a valid palindrome
     */
    public boolean isPalindrome(String s) {
        // write your code here
        if(s == null)
            return false;
        int left = 0, right = s.length() - 1;
        char[] cs = s.toCharArray();
        while(left < right){
            while(left < right && !isLetter(cs[left]))
                left ++;
            while(left < right && !isLetter(cs[right]))
                right --;
            if(Character.toLowerCase(cs[left ++]) != Character.toLowerCase(cs[right --])){
                return false;
            }
        }
        return true;
    }
    //判断字母和数字
    private boolean isLetter(char ch){
        return ((ch >= 'a' && ch <= 'z') || (ch >= 'A' && ch <= 'Z') || (ch >= '0' && ch <= '9'));
    }
}
```

