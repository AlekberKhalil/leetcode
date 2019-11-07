# braze OA

{% file src=".gitbook/assets/untitled1.png" %}

{% file src=".gitbook/assets/untitled2.png" %}

{% file src=".gitbook/assets/untitled4.png" %}

{% file src=".gitbook/assets/untitled5.png" %}

```text

import collections
class Solution:
    def getUnallottedUsers(self,bids, totalShares):
        # Write your code here
        arr = collections.defaultdict(list)
        bids.sort(key=lambda x: (-x[2],x[3]))
        for user, nshare, price, time in bids:
            arr[price].append([user, nshare, time])
        arr = sorted(arr.items(), key=lambda x: (-x[0]))
        idx = 0
        for i, group in enumerate(arr):
            group = group[1]
            if len(group) == 1:
                user, nshare, time = group[0]
                if totalShares <= nshare:
                    idx = i + 1
                    break
                totalShares -= nshare
            else:
                if totalShares  < len(group):
                    idx = i + totalShares
                    break
                totalShares -= sum(x[1] for x in group)


        res = [x[0] for x in bids[idx:]]
        return sorted(res)


    import collections
    def getTimes(self,time, direction):
        # Write your code here
        time2group = collections.defaultdict(list)
        for i, t in enumerate(time):
            time2group[t].append(i)
        res = []
        pre = -1
        n = len(time2group)
        t = 0
        for k,v in time2group.items():
            p1, p2 = [], []
            for j in v:
                t = max(t,k)
                if pre == -1 or pre == 1:
                    if direction[j] == 1:
                        p1.append(t)
                        pre = 1
                    else:
                        p2.append(t)

                else:
                    if direction[j] == 0:
                        p1.append(t)
                        pre = 0
                    else:
                        p2.append(t)
                t += 1
            res += p1 + p2
        return res
```

