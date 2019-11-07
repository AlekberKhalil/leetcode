# Minimum string array coverage

## Description

Given a string collection tag\_list, an array of strings all\_tags, find the smallest all\_tags sub-array contains all the string in the tag\_list, output the length of this sub-array. If there is no return`-1`.

```text
1 <= |tag_list|,|all_tags| <=10000All string length <= 50
```

## Example

Given tag\_list =`["made","in","china"]`, all\_tags =`["made", "a","b","c","in", "china","made","b","c","d"]`, return`3`.

```text
Explanation:["in", "china","made"] contains all the strings in tag_list,6 - 4 + 1 = 3.
```

Given tag\_list =`["a"]`, all\_tags =`["b"]`, return`-1`.

```text
Explanation:Does not exist.
```

分析

夹逼法，此题假设target里的没有duplicate，2个Map做

先m1里存所有target和count，m2用来后来增减target

右边for loop前进，如果遇到target就存入m2，直到存满所有target：m2.size\(\) = target.size\(\)，就可以开始减少left开始夹逼

夹逼的while里，一定要记得判断left也是target才能进入m2的操作

结尾记得判断如果长度就是all tags，就是不存在，返回-1

```text
public class Solution {    /**     * @param tagList: The tag list.     * @param allTags: All the tags.     * @return: Return the answer     */    public int getMinimumStringArray(String[] tagList, String[] allTags) {        // Write your code here        Map<String, Integer> m1 = new HashMap<>();        Map<String, Integer> m2 = new HashMap<>();        //先把所有target的数字都加入map        for(String s : tagList) {            m1.put(s, 1);        }        int ans = allTags.length;        int l = 0;        for(int r = 0; r < allTags.length; r++) {            //右边一直走，然后左边慢慢缩小，夹逼得方法            if(m1.containsKey(allTags[r])) {                //右边走，遇到target的存在的都加入m2                if(m2.containsKey(allTags[r])) {                     m2.put(allTags[r],  m2.get(allTags[r]) + 1);                } else {                    m2.put(allTags[r], 1);                }               //左边开始夹逼               while(l < r && m2.size() == tagList.length) {                   ans = Math.min(ans, r - l + 1);                   //l必须是target里的才行                   if(m1.containsKey(allTags[l])) {                       if(m2.get(allTags[l]) == 1) {                         m2.remove(allTags[l]);                    } else {                        m2.put(allTags[l],  m2.get(allTags[l]) - 1);                    }                   }                    l ++;               }            }        }        if(ans == allTags.length) {            return -1;        }        return ans;    }}
```

用的模板，注意最后条件 如果d=n+1的话 要返回-1。因为初始化d=n+1.

如果初始化时 float\("inf"\)，就比较d == float\("inf"\) return -1

```text
import collectionsclass Solution:    """    @param tagList: The tag list.    @param allTags: All the tags.    @return: Return the answer    """    def getMinimumStringArray(self, tagList, allTags):        # Write your code here        map = collections.defaultdict(int)        for i in tagList:            map[i] += 1        start=end=0        counter=len(tagList)        n = len(allTags)        d=n+1        while end<n:            if map[allTags[end]]>0:                counter -=1            map[allTags[end]] -= 1            end +=1            while counter == 0:                d = min(d,end-start)                if map[allTags[start]] == 0:                    counter += 1                map[allTags[start]] += 1                start += 1        if d == n+1:            return -1        return d
```

