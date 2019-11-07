# MergeSort

分析:

merge时候，注意temp长度是right-left+1,arr\[left:right+1\]=temp\[:\]

```text
class MergeSort:    def sort(self,arr):        if not arr or not len(arr):            return arr        temp = [0]*len(arr)        self.mergeSort(arr,0,len(arr)-1)        return arr    def mergeSort(self,arr,left,right):        if left >= right:            return        mid = (left+right)//2        self.mergeSort(arr,left,mid)        self.mergeSort(arr,mid+1,right)        self.merge(arr,left,mid,right)    def merge(self,arr,left,mid,right):        i = 0        temp = [0]*(right-left+1)        start = left        end = mid+1        while start<=mid and end<=right:            if arr[start] < arr[end]:                temp[i] = arr[start]                start += 1            else:                temp[i] = arr[end]                end += 1            i += 1        while start<=mid:            temp[i] = arr[start]            start += 1            i += 1        while end<=right:            temp[i] = arr[end]            end += 1            i += 1        arr[left:right+1]=temp[:]
```

