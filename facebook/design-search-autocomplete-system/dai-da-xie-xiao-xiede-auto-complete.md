# 带大写小写的auto complete

```text
给IDE设计一个autocomplete功能。给出一个如下的String[]。要求输入大写字母和几个小写字母后，实现autocomplete。大写字母必须全部match。感觉是用Trie，但怎么存怎么查没想明白。欢迎大家讨论。String[]  className {        "GraphView",        "DataGraphView",        "DataController",        "GraphViewController",        "DataScienceView"}autocomplete(String[] className, "Data");  --> {"DataGraphView", "DataController", "DataScienceView"};autocomplete(String[] className, "GVi");   -->  {"GraphView",  "GraphViewController"};autocomplete(String[] className, "GraphController");   -->  {""};
```

分析：

每个大写之间加上\*，这样小写可以任意匹配

search函数递归

1 树完了 返回

2 词完了 继续把树遍历完

3 树到hasword节点，该单词塞入

搜索词的时候，遇到\*，树动单词\*不动，直到遇到大写为止

```text
class TriNode:    def __init__(self,c):        self.c = c        self.children = {}        self.hasWord = Falseclass AutoComplete:    root = TriNode(0)    def __init__(self, strs):        for i in strs:            self.insert(i)    def insert(self,s):        cur = self.root        for i in s:            if i not in cur.children:                cur.children[i] = TriNode(i)            cur = cur.children[i]        cur.hasWord = True    def search(self,s,root,pos,path,ret):        if root.hasWord: #一个单词可加入            ret.append(path)        if not len(root.children):#树到尽头要返回            return        if pos+1>=len(s):#词到尽头 抛弃词只搜索树            for child in root.children:                self.search(s, root.children[child], pos + 1, path + root.children[child].c, ret)        else: #搜索词            if s[pos] != '*':                for child in root.children:                    if s[pos] == root.children[child].c:                        self.search(s, root.children[child], pos + 1, path + s[pos], ret)            else:                for child in root.children:                    if root.children[child].c.islower():                        self.search(s,root.children[child],pos,path+root.children[child].c,ret) #匹配*， s不动，trie一直往下走                    else:                        if s[pos + 1] == root.children[child].c:                            self.search(s,root.children[child], pos + 2, path + root.children[child].c, ret) #遇到大写，可以匹配s了    def autoComplete(self,s):        ns =[]        for i in range(len(s)):            if i!=0 and s[i].isupper():                ns.append('*')                ns.append(s[i])            else:                ns.append(s[i])        ns.append('*')        s = ''.join(ns)        ret = []        self.search(s,self.root,0,"",ret)        return ret
```

