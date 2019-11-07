# Radius\_union find\_same name

```text
import java.io.IOException;
import java.util.*;

class NameCount{
    String name;
    int count;
    boolean isFather = true;

    public boolean isFather() {
        return isFather;
    }

    public void setFather(boolean father) {
        isFather = father;
    }

    public NameCount(String name, int count){
        this.name = name;
        this.count = count;
    }

    public String getName() {
        return name;
    }

    public int getCount() {
        return count;
    }

    public void setName(String name) {
        this.name = name;
    }

    public void setCount(int count) {
        this.count = count;
    }

    public boolean equals(NameCount a){
        return this.name.equals(a.getName());
    }
}

class UnionFind{
    HashMap<NameCount, NameCount> father;

    public UnionFind(Map<String, NameCount> ncList){
        father = new HashMap<NameCount, NameCount>();
        for(Map.Entry<String, NameCount> e : ncList.entrySet()){
            father.put(e.getValue(), e.getValue());
        }
    }

    private NameCount find(NameCount a){
        if(father.get(a).equals(a)){
            return a;
        }
        NameCount temp = find(father.get(a));
        father.put(a, temp);
        return temp;
    }

    public void connect(NameCount a, NameCount b){
        NameCount root_a = find(a);
        NameCount root_b = find(b);
        if(!root_a.equals(root_b)){
            father.put(root_b, root_a);
            root_a.setCount(root_b.getCount() + root_a.getCount());
            root_a.setFather(true);
            root_b.setFather(false);
        }
    }


}
public class Solution {
    public Map<String, Integer> getpairCount(String[][] arr, Map<String, Integer> pairs){
        Map<String, Integer> ret = new HashMap<String, Integer>();

        if(arr == null || arr[0] == null || arr.length == 0 || arr[0].length == 0)
            return ret;
        //key and value is name and corresponding NameCount object
        Map<String, NameCount> map = new HashMap<String, NameCount>();
        //initiate the UnionFind class with all names and counts
        for(int i = 0; i < arr.length; i++) {
            for (int j = 0; j < arr[i].length; j++) {
                if(pairs.containsKey(arr[i][j]) && !map.containsKey(arr[i][j])){
                    NameCount cur = new NameCount(arr[i][j], pairs.get(arr[i][j]));;
                    map.put(arr[i][j], cur);
                }
            }
        }

        UnionFind uf = new UnionFind(map);
        //connect the names that belongs to one group.
        NameCount prev = null, cur = null;
        for(int i = 0; i < arr.length; i++) {
            for (int j = 0; j < arr[i].length; j++) {
                cur = map.get(arr[i][j]);
                if(prev != null){
                    uf.connect(prev, cur);
                }
                prev = cur;
            }
            prev = null;
        }
        //save the result with main name and total of this name group
        for(Map.Entry<String, NameCount> e : map.entrySet()){
            NameCount nc = e.getValue();
            if(nc.isFather){
                ret.put(nc.getName(), nc.getCount());
            }
        }

        return ret;
    }
    public static void main(String[] args) throws IOException {
        Solution s  = new Solution();
        String[][] arr = {{"jane","janny"}, {"janny", "jannifer"}, {"sara", "sarah"}, {"mike", "michael"}, {"jane", "jannie"}};
        Map<String, Integer> pairs = new HashMap<String, Integer> ();
        pairs.put("jane", 2);
        pairs.put("janny", 5);
        pairs.put("jannifer", 3);
        pairs.put("sara", 6);
        pairs.put("sarah", 1);
        pairs.put("mike", 4);
        pairs.put("michael", 6);
        pairs.put("jannie", 3);

        Map<String, Integer> ret = s.getpairCount(arr,  pairs);
        for(Map.Entry<String, Integer> e : ret.entrySet()){
            System.out.println("Group Name: " + e.getKey() + " total: " + e.getValue());
        }

    }
}
```

