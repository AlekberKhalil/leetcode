# Get Relations

一群人的关系，给出2个人 输出所有可能关系，用Map建有向图，dfs遍历有向图。感觉多条路径时候bfs不能做。



```text
def getRelations(arr,a,b):    mm = {}    for x,r,y in arr:        if x not in mm:            mm[x] = [[y,r]]        else:            mm[x].append([y,r])    seen = set()    res = []    def dfs(x,path):        if x == b:            res.append(path)            return        if x in mm:            for y,r in mm.get(x):                if y not in seen:                    dfs(y,path + [r,y])    dfs(a,[a])    print(res)getRelations([["br","bro","lis"],              ["br","son","hom"],              ["lis","dau","hom"],              ["mar","wife","hom"]],"br","hom")
```

