# Letter Case Permutation\(DFS\)

Given a string S, we can transform every letter individually to be lowercase or uppercase to create another string. Return a list of all possible strings we could create.

```text
Examples:
Input:
 S = "a1b2"

Output:
 ["a1b2", "a1B2", "A1b2", "A1B2"]


Input:
 S = "3z4"

Output:
 ["3z4", "3Z4"]


Input:
 S = "12345"

Output:
 ["12345"]
```

**Note:**

* `S`will be a string with length at most`12`

  .

* `S`will consist only of letters or digits.

分析

DFS。Stringbuilder做路径。 这里没有for loop但是有2条路，大写一条路小写一条路。

```text
class Solution {
    public List<String> letterCasePermutation(String S) {
        List<String> ret = new ArrayList<>();
        StringBuilder sb = new StringBuilder();
        dfs(S,ret,sb,0);
        return ret;
    }

    void dfs(String S, List<String> ret, StringBuilder sb, int pos){
        if(pos == S.length()){
            String path = sb.toString();
            if(!ret.contains(path)){
                ret.add(path);
            }

            return;
        }

        sb.append(Character.toLowerCase(S.charAt(pos)));
        dfs(S,ret,sb,pos+1);
        sb.deleteCharAt(sb.length()-1);

        sb.append(Character.toUpperCase(S.charAt(pos)));
        dfs(S,ret,sb,pos+1);
        sb.deleteCharAt(sb.length()-1);
    }
}
```

