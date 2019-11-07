# anagram

search anagram in the source word

比如 ccccta cat return index: cta :cat

```text
import collections# variable used: Two Pointer start and end with fixed length of target string. Two Map records character and counter for both source string and target string# 1. End pointer always ahead of start pointer. End pointer keep going until: 1 end pointer reach to the end, 2 meet the fixed length of target string.# 2. Check if the answer is found, otherwise increase the start pointer and update source map, then go back to step 1# 3. Valid function compares the count of each char for two map.#test case#"dog","odg"   ->  0# 'am','aa'    ->  -1# 'caa','a'   ->   1# '',''    ->  0# 'a','a'    ->  0# 'a','ac'    ->  -1# "cccctcaaattt","cat"   ->   4class Solution:    def subsetsWithDup(self, source,target):        """        :type nums: List[int]        :rtype: List[List[int]]        """        if not source and not target:            return 0        if not source or not target:            return -1        tcount = {} #character and counter for target string        scount = {} #character and counter for source string        for i in target:            tcount[i] = tcount.get(i,0) + 1        l =end = 0 # two pointer start and end        sn,tn = len(source),len(target) # length of target and source string        while l < sn:            if end < l:                end = l            #   update end pointer            while end < sn and end - l < tn:                scount[source[end]] = scount.get(source[end],0)+1                end += 1            #  return result if exists            if end<= sn and self.isValid(scount,tcount):                return l            #   update start pointer            scount[source[l]] -= 1            l += 1        return -1    def isValid(self,source,target):        for i in target.keys():            if i not in source or target[i] != source[i]:                return False        return True
```

