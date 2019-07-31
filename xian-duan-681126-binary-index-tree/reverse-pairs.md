# Reverse Pairs

Given an array`nums`, we call`(i, j)`an**important reverse pair**if`i < j`and`nums[i] > 2*nums[j]`.

You need to return the number of important reverse pairs in the given array.

**Example1:**

```text
Input
: [1,3,2,3,1]

Output
: 2
```

**Example2:**

```text
Input
: [2,4,3,5,1]

Output
: 3
```

**Note:**

1. The length of the given array will not exceed

   `50,000`

   .

2. All the numbers in the input array are in the range of 32-bit integer.

分析

顺序loop数，所以当前数字来的时候，只能和它前面的数字比较它的2x+1

和前面count of smaller number,用map存数字和ordered index。本题直接排序再用二分查找。

BIT

update 和query反过来，update更新比它小的index，query取比它大的，然后正序loop。本题就是要找比J小的I,所以update每次更新的Index都是比当前小的

```text
class Solution:
    def reversePairs(self, nums: List[int]) -> int:
        n = len(nums)
        copy = sorted(nums)
        bitTree = [0] *(n+1)
        def update(i):
            while i > 0:
                bitTree[i] += 1
                i-=i&-i

        def getCnt(i):
            sm = 0
            while i < n+1:
                sm +=bitTree[i]
                i+=i&-i
            return sm

        res = 0
        for i in nums:
            res += getCnt(bisect.bisect_left(copy, i*2+1)+1)
            update(bisect.bisect_left(copy, i)+1)
        return res
```

普通思路，这里Getcnt后面做法不同

因为Update高位集合了低位的和，所以 query\(n\) -query\(2x+1\)得到2x+1-n之间的所有数字。

```text
class Solution:
    def reversePairs(self, nums: List[int]) -> int:
        n = len(nums)
        copy = sorted(nums)
        bitTree = [0] *(n+1)
        def update(i):
            while i < n+1:
                bitTree[i] += 1
                i+=i&-i

        def getCnt(i):
            sm = 0
            while i >0:
                sm += bitTree[i]
                i-=i&-i
            return sm
        res = 0
        for i in nums:
            res += getCnt(n) - getCnt(bisect.bisect_left(copy, i*2+1)) #所有2x+1 - n之间的数都，>2x+1的所有数，不是一个数。
            update(bisect.bisect_left(copy, i)+1)
        return res
```

分治

左右段mergesory后，左半端和右半段比较得count。同时左右半段sort merge

```text
class Solution:
    def reversePairs(self, nums: List[int]) -> int:
        def mergeSort(s,e):
            if s >= e:
                return 0  
            mid = (s+e)//2
            res  = mergeSort(s,mid) + mergeSort(mid+1,e)
            i,j,k =0,mid+1,mid+1
            temp=[]
            for i in range(s,mid+1):                
                while j <=e and nums[i] > nums[j]*2: 
                    j += 1 
                res+=(j-mid-1)
                while k <=e and nums[i] >= nums[k]:                     
                    temp.append(nums[k])
                    k +=1
                temp.append(nums[i])


            nums[s:s+len(temp)] = temp[:]
            return res


        return mergeSort(0,len(nums)-1)
```

