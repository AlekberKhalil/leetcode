# Encode and Decode TinyURL



> Note: This is a companion problem to the [System Design](https://leetcode.com/discuss/interview-question/system-design/) problem: [Design TinyURL](https://leetcode.com/discuss/interview-question/124658/Design-a-URL-Shortener-%28-TinyURL-%29-System/).

TinyURL is a URL shortening service where you enter a URL such as `https://leetcode.com/problems/design-tinyurl`and it returns a short URL such as `http://tinyurl.com/4e9iAk`.

Design the `encode` and `decode` methods for the TinyURL service. There is no restriction on how your encode/decode algorithm should work. You just need to ensure that a URL can be encoded to a tiny URL and the tiny URL can be decoded to the original URL.

分析

可以直接用urls的len，urls存所有longurl。可以decode回去，直接得到index取出longurl

用某个数字mod62，然后取\[A-Z, a-z, 0-9\]间值。 这个数字可以用global counter或者len\(urls\).不能decode，只能把所有decoded short-&gt;long map存起来，decode直接取

别忘了存2个map，对重复longurl不用encode again

```text
class Codec:
    def __init__(self):
        self.global_counter = 0 
        self.s2l = {}
        self.l2s = {}
        self.base = 'http://tinyurl.com/'
        self.strs = string.ascii_letters+string.digits

    def encode(self, longUrl):
        """Encodes a URL to a shortened URL.
        
        :type longUrl: str
        :rtype: str
        """       
           
        if longUrl not in self.l2s:        
            encoded = ''.join(random.choice(self.strs) for i in range(6))
            self.s2l[encoded] = longUrl
            self.l2s[longUrl] = encoded
            self.global_counter += 1
            return self.base + encoded
        else:
            return self.base+self.l2s[longUrl]
               
        

    def decode(self, shortUrl):
        """Decodes a shortened URL to its original URL.
        
        :type shortUrl: str
        :rtype: str
        """
        decoded = shortUrl[-6:]#shortUrl.split('/')[-1]
        return self.s2l[decoded]
        
    
#     def __init__(self):
#         self.urls = []

#     def encode(self, longUrl):
#         self.urls.append(longUrl)
#         return 'http://tinyurl.com/' + str(len(self.urls) - 1)

#     def decode(self, shortUrl):
#         return self.urls[int(shortUrl.split('/')[-1])]
        

# Your Codec object will be instantiated and called as such:
# codec = Codec()
# codec.decode(codec.encode(url))
```



