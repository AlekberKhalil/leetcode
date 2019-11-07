# Read N Characters Given Read4 II - Call multiple times

The API:`int read4(char *buf)`reads`4`characters at a time from a file.

The return value is the actual number of characters read. For example, it returns 3 if there is only 3 characters left in the file.

By using the read4 API, implement the function`int read(char *buf, int n)`that reads n characters from the file.

分析

缓冲区size 4，每次read4读入。

如果readpos == writepos 又要读入buffer，同时readpos writepos重设

如果writepos ==0 \(read4 return0）没有数据了返回

```text
"""
The read4 API is already defined for you.
@param buf a list of characters
@return an integer
you can call Reader.read4(buf)
"""


class Solution:
    buffer = [0]*4
    write=readi = 0

    # @param {char[]} buf destination buffer
    # @param {int} n maximum number of characters to read
    # @return {int} the number of characters read
    def read(self, buf, n):
        # Write your code here
        for i in range(n):
            if self.readi == self.write:
                self.write = Reader.read4(self.buffer)
                self.readi = 0
                if self.write == 0:
                    return i
            buf[i]=self.buffer[self.readi]
            self.readi +=1


        return n
```

