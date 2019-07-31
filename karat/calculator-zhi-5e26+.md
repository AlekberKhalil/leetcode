# karat calculator 三题

分析

这类计算题题目，带\*\就用数字带符号压入栈

带括号就sign 1和-1每次相乘，然后+1,-1压入栈

```text
class Calculator:
    def calculate(self,strs): #1+2-3
        sign = 1
        num = 0
        res = 0
        for i in strs:
            if i.isdigit():
                num = num*10+int(i)
            if i == '+':
                res+=sign*num
                sign=1 #定的是将来的符号
                num = 0
            if i == '-':
                res += sign * num
                sign = -1
                num = 0
        if num:
            res += sign * num #不要忘了最后一个符号
        return res

c = Calculator()
ret = c.calculate("1999")
print(ret)
```

题目

第一題是給你一個string例如"2+3-999"回傳計算結果  
第二題加上parenthesis例如"2+\(\(8+2\)+\(3-999\)\)"一樣回傳計算結果  
第三道题是加了变量名的。。会给你一个map比如{'a':\`1, 'b':2, 'c':3}，假设输入为"a+b+c+1"输出要是7，如果有未定义的变量，比如"a+b+c+1+d"输出就是7+d

分析

1,3不用stack，1用sign， 3用op str

2带括号或者\*、需要stack，sign +1 -1

```text
class Calculator:
    def calculate(self,strs): #1+2-3
        sign = 1
        num = 0
        res = 0
        for i in strs:
            if i.isdigit():
                num = num*10+int(i)
            if i == '+':
                res+=sign*num
                # this op is for future
                sign=1
                num = 0
            if i == '-':
                res += sign * num
                sign = -1
                num = 0
        if num:
            res += sign * num #don't forget last number
        return res

#with stack
    def calculate2(self,strs):
        stack = []
        sign = 1
        num = res = 0
        for i in strs:
            if i.isdigit():
                num += num * 10 + int(i)
            elif i == '(':
                stack.append(res)
                stack.append(sign)
                sign = 1
                res = 0
            elif i == ')':
                res += num * sign
                res = res*stack.pop()+stack.pop()
                num = 0

            elif i in '+-':
                res += sign*num
                num = 0
                sign = 1 if i == '+' else -1
        if num:
            res += sign * num
        return res


#with map
    def calculate3(selfself,strs,map):
        num=res =0
        snum =[]
        op = "+"
        for i in strs:
            if i.isdigit():
                num = num*10+int(i) #not =+ wrong every time!!!!!!
            elif i.isalpha():
                if i in map:
                    num = map[i]
                else:
                    snum.append(op+i)
            elif i in '+-':
                if i == '+':
                    res += num
                else:
                    res-= num
                num = 0
                op = i
        if num:
            if op == '+':
                res += num
            else:
                res -= num
        return str(res) + ''.join(snum)





#
c = Calculator()
# ret = c.calculate("")#2+((8+2)+(3-999))
# print(ret)

ret = c.calculate2("2+((8+2)+(3-999))")
#ret = c.calculate3("x+a+b+f+c+1+d",{'a':1, 'b':2, 'c':3})#2+((8+2)+(3-999))
print(ret)
```

