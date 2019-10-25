# Expedia oa

```text
import math


class Solution:
    def breakPlindrome(self,s):
        n = len(s)
        updated = False
        for i in range(n//2+1):
            if s[i]!='a':
                s[i] = 'a'
                updated = True
                break
        return s if updated else 'impossible'


    def vowel(self,s,indexs):
        vowels = set('aeiou')
        isVowel = []
        res = []
        for w in s:
            if w[0] in vowels and w[-1] in vowels:
                isVowel.append(True)
            else:
                isVowel.append(False)
        for q in indexs:
            a,b = q.strip('[]').split('-')
            cnt = 0
            for i in range(int(a)-1, int(b)):
                cnt += 1 if isVowel[i] else 0
            res.append(cnt)
        return res

    def pthFactor(self,n,p):
        s = int(math.sqrt(n))
        res =[]
        for i in range(1,s+1):
            if not n % i:
                if i*i == n:
                    res.append(i)
                else:
                    res.append(i)
                    res.append(n//i)
        res.sort()
        return res[p-1] if len(res) >=p else res[-1]

    def mergeStr(self,a,b):
        n,m = len(a),len(b)
        i=j=0
        res =[]
        while i < n or j < m:
            if i < n:
                res.append(a[i])
                i+=1
            if j < m:
                res.append(b[j])
                j+=1
        return ''.join(res)




    def mathProblem(self, maths, threshhold):
        i,n=0,len(maths)
        res= [maths[0]]
        while i < n-1:
            if i+2 < n and maths[i+1] < maths[i+2]:
                res.append(maths[i+2])
                i = i+2
            else:
                res.append(maths[i+1])
                i = i+1
            if res[-1] - res[0] >= threshhold:
                return len(res)
        return len(maths)





def maxSum(arr, threshold):
    # Write your code here
    res = float('-inf')
    n = len(arr)
    arr.sort()
    def dfs(pos, curSum):
        nonlocal res
        if curSum == 0:
            res = threshold
            return
        res = max(res, threshold - curSum)
        if pos == n:
            return
        for i in range(pos,n):
            if arr[i] <= curSum:
                res = max(res, threshold - curSum)
                dfs(i+1, curSum - arr[i])
    dfs(0,threshold)
    return res







```

