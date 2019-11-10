# embold html

先merge所有Intervals，然后取空闲区域

```text
import re #regular expression library
def emboldenHTML(input, boldenStrs):
    if not boldenStrs:
        return input
    indexs = [] # start and end indexes of bolden strings in the input
    for pattern in boldenStrs:
        indexs += [[m.start(),m.end()] for m in re.finditer(pattern,input)] # use regular expression to find out all the occurance of bolden strings

    indexs.sort() # sort the indexs of boldens strings, start index ascending or end index ascending
    merged = [] # merged indexes of bolden strings

    # loop through sorted indexes and merged overlappedd ranges
    for i in range(len(indexs)):
        start,end = indexs[i]
        if not merged or indexs[i-1][1] < start:
            merged.append([start,end])
        else:
            merged[-1][1] = end

    lastpos = 0 # keep track of the last position in the input
    res = ''

    # add <b></b> to bolden strs in the input and print result
    for i in range(len(merged)):
        start,end = merged[i]
        # add plain text before the current bolden string, which is between the lastpos and current bolden string's start position
        if lastpos < start:
            res += input[lastpos:start]
        #add the bolden string
        res += '<b>' + input[start:end] + '</b>'
        #update the last position in the input
        lastpos = end

    # add the remaining string in the input
    if lastpos < len(input):
        res += input[lastpos:]

    print(res) # print the result

#test case
emboldenHTML('abcd77abcab',['ab','abc']) # output: <b>abc</b>d77<b>abcab</b>
emboldenHTML('hyatt35342hy',['hy','hyat']) # output: <b>hyat</b>t35342<b>hy</b>
```

