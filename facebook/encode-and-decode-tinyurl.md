# Encode and Decode TinyURL

Note: This is a companion problem to the

> [System Design](https://leetcode.com/discuss/interview-question/system-design/) problem: [Design TinyURL](https://leetcode.com/discuss/interview-question/124658/Design-a-URL-Shortener-%28-TinyURL-%29-System/) .

TinyURL is a URL shortening service where you enter a URL such as`https://leetcode.com/problems/design-tinyurl`and it returns a short URL such as`http://tinyurl.com/4e9iAk`.

Design the`encode`and`decode`methods for the TinyURL service. There is no restriction on how your encode/decode algorithm should work. You just need to ensure that a URL can be encoded to a tiny URL and the tiny URL can be decoded to the original URL.

分析

1. string.ascii\_letters+string.digits 提供了可选的字符
2. ''.join\(random.choice\(chars\) for \_ in range\(6\)\)得到了code
3. 2个map code2url 和url2code
4. encode时候有个while longURL not in url2code 保证了code重复情况下依然可以create新code

```text
class Codec:    alphabet = string.ascii_letters+string.digits    code_base = "http://tinyurl.com/"    def __init__(self):        self.url2code = {}        self.code2url = {}    def encode(self, longUrl):        """Encodes a URL to a shortened URL.        :type longUrl: str        :rtype: str        """        while longUrl not in self.url2code:            code = ''.join(random.choice(self.alphabet) for _ in range(6))            if code not in self.code2url:                self.code2url[code] = longUrl                self.url2code[longUrl] = code        return self.code_base + code    def decode(self, shortUrl):        """Decodes a shortened URL to its original URL.        :type shortUrl: str        :rtype: str        """        return self.code2url[shortUrl[-6:]] # Your Codec object will be instantiated and called as such:# codec = Codec()# codec.decode(codec.encode(url))
```

