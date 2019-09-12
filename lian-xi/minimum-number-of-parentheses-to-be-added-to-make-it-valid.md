# Minimum number of Parentheses to be added to make it valid

Given a string S of parentheses ‘\(‘ or ‘\)’ where, ![0\leq len\(S\)\leq 1000](https://www.geeksforgeeks.org/wp-content/ql-cache/quicklatex.com-62045758c8e8fa096f4efb374625c2cf_l3.svg). The task is to find minimum number of parentheses ‘\(‘ or ‘\)’ \(at any positions\) we must add to make the resulting parentheses string is valid.

**Examples:**

```text
Input: str = "())"
Output: 1
One '(' is required at beginning.

Input: str = "((("
Output: 3
Three ')' is required at end.
```

分析

balance表示左右差，-1时候右边加\) +时候左边加\(

最后这里答案是bal（多余的正数代表多余左括号）， ans代表需要的右括号。 记得每次ans++， bal也要update

```text
ef minParentheses(p): 
      
    # maintain balance of string  
    bal=0
    ans=0
    for i in range(0,len(p)): 
        if(p[i]=='('): 
            bal+=1
        else: 
            bal+=-1
              
        # It is guaranteed bal >= -1 
        if(bal==-1): 
            ans+=1
            bal+=1
    return bal+ans 
```

