# Read N Characters Given Read4

```text
class Solution:    def read(self,buf,n):        buffer = [0]*4        readi = pos = 0        while True:            size = read4(buffer)            readi = 0            while readi < size and pos < n:                buf [pos] = buffer[readi]                readi += 1                pos+=1            if size == 0 or pos == n:                return pos
```

