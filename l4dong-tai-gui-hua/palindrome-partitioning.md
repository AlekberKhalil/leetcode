# Palindrome Partitioning

Given a strings, partitionssuch that every substring of the partition is a palindrome.

Return all possible palindrome partitioning ofs.

For example, givens=`"aab"`,  
Return

```text
[  ["aa","b"],  ["a","a","b"]]
```

分析

DP+DFS.

带有Pos的DFS：每次有palindrome，就加入path，然后从index+1后来开始继续dfs。

```text
class Solution {    public List<List<String>> partition(String s) {        List<List<String>> ret = new ArrayList<>();        if(s == null || s.length() == 0)            return ret;        List<String> path = new ArrayList<String>();        boolean[][] isP = isPalindrome(s);                dfs(s, path, ret, 0, isP);        return ret;    }    void dfs(String s, List<String> path, List<List<String>> ret, int pos, boolean[][] isP){        if(pos == s.length()){            ret.add(new ArrayList<String>(path));            return;        }        for(int i = pos; i < s.length(); i ++){            if(isP[pos][i]){//包含I                path.add(s.substring(pos, i + 1));                dfs(s, path,ret, i + 1, isP);//i+1 这样才能到pos=n最后，否则只到i-1                path.remove(path.size() - 1);            }        }    }    boolean[][] isPalindrome(String s){        int n = s.length();        boolean[][] isP = new boolean[n][n];        for(int i = 0; i < n; i ++){            isP[i][i] = true;            for(int j = 0; j < i; j ++){                    isP[j][i] = s.charAt(i) == s.charAt(j) && (i - j < 2 || isP[j + 1][i - 1]);            }        }        return isP;    }}
```

