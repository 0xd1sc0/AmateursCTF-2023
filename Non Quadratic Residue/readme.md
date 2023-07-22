## Non Quadratic Residue

## chall
- [main.py]()
- [out.txt]()
  
## solution
In the challange the value of p is calculated as getModPrime(difficulty**10) . The p generated by this function is a prime which is greater than difficulty**10 .
The ciphertext c is then calculated as `c = inverse(flag, b)` and n is calculated as `n = pow(c, difficulty, b)`.
Here e is 210 which is a small number . Since ` p**e < n ` we tried finding the nth root .  So we try to find all the 210th roots of c in the field F.<br>

## solve.py
```py
from Crypto.Util.number import *
p = 135954424160848276393136392848608760791498666756786983317146989739232222268153235587604168914827859099133726281621143020610041450200631778336472889038077986687446107427527703447531968569919642975653169056203851297117178187249653136191818357235077367060617558261023389453028554177668515375377299577050000000001

F = GF(p)
 
assert is_prime(p)
c = F(13350651294793393689107684390908420972977381011191079381202728507002264420264784588373703945341668404762890725356808809021906408198983625375190500172144348596288910240548668158058030780501343680214713780242304547715977777103636873360269427453504233184515002477489763359569764117968027273137245802436961373256)

l = c.nth_root(210,all=True)
for i in l:
    if gcd(int(i),p) == 1:
        try:
            print(long_to_bytes(inverse(int(i),p)).decode())
            print("---------------------------------")
        except:
            pass
```