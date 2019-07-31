# Word Search II

Given a matrix of lower alphabets and a dictionary. Find all words in the dictionary that can be found in the matrix. A word can start from any position in the matrix and go left/right/up/down to the adjacent position.

**Example**

Given matrix:

```text
doaf
agai
dcan
```

and dictionary:

```text
{"dog", "dad", "dgdg", "can", "again"}
```

return {"dog", "dad", "can", "again"}

分析：

初始就判断valid,因为叶节点也没必要继续扩展下去。同时剪枝是在for loop外，为了一个元素的时候也能判断。

```text
public class Solution {
    /**
     * @param board: A list of lists of character
     * @param words: A list of string
     * @return: A list of string
     */
     class TrieNode {
        String s;
         boolean isString;
         HashMap<Character, TrieNode> subtree;
         public TrieNode() {
            // TODO Auto-generated constructor stub
             isString = false;
             subtree = new HashMap<Character, TrieNode>();
             s = "";
         }
    };


    class TrieTree{
        TrieNode root ;
        public TrieTree(TrieNode TrieNode) {
            root = TrieNode;
        }
        public void insert(String s) {
            TrieNode now = root;
            for (int i = 0; i < s.length(); i++) {
                if (!now.subtree.containsKey(s.charAt(i))) {
                    now.subtree.put(s.charAt(i), new TrieNode());
                }
                now  =  now.subtree.get(s.charAt(i));
            }
            now.s = s;
            now.isString  = true;
        }
        public boolean find(String s){
            TrieNode now = root;
            for (int i = 0; i < s.length(); i++) {
                if (!now.subtree.containsKey(s.charAt(i))) {
                    return false;
                }
                now  =  now.subtree.get(s.charAt(i));
            }
            return now.isString ;
        }
    };

     ArrayList<String> ret;
     char[][] board;
     int n,m;
     int[] dx = {1,-1,0,0};
     int[] dy = {0,0,1,-1};

     public void search(int x, int y, TrieNode root){

         if(root.isString == true){
             if(!ret.contains(root.s)){
                 ret.add(root.s);
             }
         }
//只能在此判断是为了只有一个元素的时候，在for里判断直接continue不会进行下一轮dfs。这里初始就判断是否valid.
         if(x < 0 || x >= n || y < 0 || y >= m || board[x][y]==0 || root ==null)
            return;

        if(root.subtree.containsKey(board[x][y])){
            for(int i = 0; i < 4; i ++){
                char temp = board[x][y];
                board[x][y] = 0;
                search(x+dx[i], y+dy[i], root.subtree.get(temp));
                board[x][y] = temp;
            }
        }
     }

    public ArrayList<String> wordSearchII(char[][] board, ArrayList<String> words) {
        // write your code here

        this.ret = new ArrayList<String>();
        this.board = board;
        this.n = board.length;
        this.m = board[0].length;

        TrieTree tree = new TrieTree(new TrieNode());
        for(String word : words){
            tree.insert(word);
        }

        for(int i = 0; i< board.length; i++){
            for(int j=0; j< board[0].length; j++){
                search(i, j, tree.root);

            }
        }
        return ret;

    }
}
```

