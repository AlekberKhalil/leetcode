# Accounts Merge\(Union Find\)

Given a list`accounts`, each element`accounts[i]`is a list of strings, where the first element`accounts[i][0]`is aname, and the rest of the elements areemailsrepresenting emails of the account.

Now, we would like to merge these accounts. Two accounts definitely belong to the same person if there is some email that is common to both accounts. Note that even if two accounts have the same name, they may belong to different people as people could have the same name. A person can have any number of accounts initially, but all of their accounts definitely have the same name.

After merging the accounts, return the accounts in the following format: the first element of each account is the name, and the rest of the elements are emails**in sorted order**. The accounts themselves can be returned in any order.

**Example 1:**

```text
Input:accounts = [["John", "johnsmith@mail.com", "john00@mail.com"], ["John", "johnnybravo@mail.com"], ["John", "johnsmith@mail.com", "john_newyork@mail.com"], ["Mary", "mary@mail.com"]]Output: [["John", 'john00@mail.com', 'john_newyork@mail.com', 'johnsmith@mail.com'],  ["John", "johnnybravo@mail.com"], ["Mary", "mary@mail.com"]]Explanation:The first and third John's are the same person as they have the common email "johnsmith@mail.com".The second John and Mary are different people as none of their email addresses are used by other accounts.We could return these lists in any order, for example the answer [['Mary', 'mary@mail.com'], ['John', 'johnnybravo@mail.com'], ['John', 'john00@mail.com', 'john_newyork@mail.com', 'johnsmith@mail.com']] would still be accepted.
```

**Note:**

```text
The length of accounts will be in the range [1, 1000].The length of accounts[i] will be in the range [1, 10].The length of accounts[i][j] will be in the range [1, 30].
```

分析

初始时，每个account的email指向第一个email做父。然后Union所有email的父。 father map-&gt; email : email\[0\]

需要建立map name到每个父， map-&gt; 父 ： name

最后merge所有父到总父，map-&gt;总父 ： list of 父

本题顺序写半天，最后用linkedhashmap.

```text
class Solution {    Map<String,String> father = null;    public List<List<String>> accountsMerge(List<List<String>> accounts) {        //map root to name        Map<String, String> nameMap = new LinkedHashMap<>();        //group each root of account to the root        Map<String, Set<String >> groupRoot = new LinkedHashMap <>();        father = new LinkedHashMap<>();        init(accounts,nameMap);        List<List<String>> ret = new ArrayList<>();        //merge accounts with same root        for(String f : father.keySet()){            String root = find(f);            if(!groupRoot.containsKey(root)){                groupRoot.put(root,new TreeSet<>());            }            Set<String> rl = groupRoot.getOrDefault(root, new TreeSet<>());            if(!root.equals(f)){                rl.add(f);            }else{                rl.add(root);            }        }        for(String r : groupRoot.keySet()){            List<String> arr = new ArrayList<>();            arr.add(nameMap.get(r));            arr.addAll(groupRoot.get(r));            ret.add(arr);        }        return ret;    }    void init(List<List<String>> accounts, Map<String, String> nameMap){        for(List<String> a :  accounts){            String name = a.get(0);            nameMap.put(a.get(1), name);            for(int i = 1; i < a.size(); i ++){                if(!father.containsKey(a.get(i))){                    father.put(a.get(i), a.get(1));                }else{                    union(a.get(1), a.get(i));                }            }        }    }    void union(String s1, String s2){        String f1 = find(s1);        String f2 = find(s2);        if(!f1.equals(f2)){            father.put(f2,f1);        }    }    String find(String s){        if(father.get(s).equals(s)){            return s;        }        father.put(s, find(father.get(s)));        return father.get(s);    }}
```

Python

```text
# Input:## accounts = [["John", "johnsmith@mail.com", "john00@mail.com"], ["John", "johnnybravo@mail.com"], ["John", "johnsmith@mail.com", "john_newyork@mail.com"],# ["Mary", "mary@mail.com"]]## Output:#  [["John", 'john00@mail.com', 'john_newyork@mail.com', 'johnsmith@mail.com'],  ["John", "johnnybravo@mail.com"], ["Mary", "mary@mail.com"]]import collectionsclass Solution:    def accountsMerge(self, accounts):        """        :type accounts: List[List[str]]        :rtype: List[List[str]]        """        self.parent = collections.defaultdict(str)        self.emailToName = collections.defaultdict(str)        for a in accounts:            name = a[0]            emails = a[1:]            self.emailToName[emails[0]] = name            for e in emails:                if not self.parent[e]:                    self.parent[e] = emails[0]                else:                    self.union(self.parent[e],emails[0])        ret = [[x for x in self.parent.keys() if self.parent.get(x) == i] for i in set(self.parent.values())]        # for i in set(self.parent.values()):        #     temp = []        #     temp.append(self.emailToName.get(i))        #     temp.extend([x for x in self.parent.keys() if self.parent.get(x) == i])        #     ret.append(temp)        return ret    def find(self, x):        if x == self.parent.get(x):            return x        self.parent[x] = self.find(self.parent.get(x))        return self.parent.get(x)    def union(self, a, b):        r_a = self.find(a)        r_b = self.find(b)        r_a = self.parent[r_b]obj = Solution()ret = obj.accountsMerge([["John", "johnsmith@mail.com", "john00@mail.com"], ["John", "johnnybravo@mail.com"], ["John", "johnsmith@mail.com", "john_newyork@mail.com"], ["Mary", "mary@mail.com"]])print (ret)
```

