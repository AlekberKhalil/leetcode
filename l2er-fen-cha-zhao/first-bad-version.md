# First Bad Version

You are a product manager and currently leading a team to develop a new product. Unfortunately, the latest version of your product fails the quality check. Since each version is developed based on the previous version, all the versions after a bad version are also bad.

Suppose you have`n`versions`[1, 2, ..., n]`and you want to find out the first bad one, which causes all the following ones to be bad.

You are given an API`bool isBadVersion(version)`which will return whether`version`is bad. Implement a function to find the first bad version. You should minimize the number of calls to the API.

分析

二分

往后都是bad，所以每次移动end，然后判断start，再end

```text
/* The isBadVersion API is defined in the parent class VersionControl.      boolean isBadVersion(int version); */public class Solution extends VersionControl {    public int firstBadVersion(int n) {        int s = 1, e = n;        while(s + 1 < e){            int m = s + (e - s)/2;            if(isBadVersion(m)){                e = m;            }else{                s = m;            }        }        if(isBadVersion(s))            return s;        else            return e;    }}
```

```text
class Solution:    def firstBadVersion(self, n):        """         :type n: int        :rtype: int        """        s,e=0,n        while s+1<e:            m = s+(e-s)//2            if isBadVersion(m):                e = m            else:                s = m        return s if isBadVersion(s) else e
```

花花木板 左闭右开

```text
class Solution:    def firstBadVersion(self, n):        """        :type n: int        :rtype: int        """        s,e = 1,n#因为是开区间，所以应该是N+1，但是怕溢出。        while s < e:            m = s + (e-s)//2            if isBadVersion(m):                e = m            else:                s = m + 1        return s
```

