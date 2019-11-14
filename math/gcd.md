# GCD

```text
static int gcd(int a, int b) 
    { 
        if (a == 0) 
            return b; 
        return gcd(b % a, a); 
    } 
```



## find GCD of floating point numbers

```text
def gcd(a,b) : 
    if (a < b) : 
        return gcd(b, a) 
      
    # base case 
    if (abs(b) < 0.001) : 
        return a 
    else : 
        return (gcd(b, a - math.floor(a / b) * b)) 
```

